# OAuth 2.0 Device Authorization Grant (RFC 8628)

The **OAuth 2.0 Device Authorization Grant** (often called the **device flow**) is an OAuth 2.0 extension designed for **input-constrained** or **browserless** devices (e.g., smart TVs, media consoles, printers) that need to obtain an access token on behalf of a user. Instead of completing the authorization interaction on the device itself, the user completes the approval step on a separate device (such as a phone or computer) with a full browser and better input capabilities.[^rfc8628]

In agentic systems, a device-flow-style interaction is sometimes used when an autonomous or semi-autonomous client needs to obtain delegated access, but cannot present an interactive browser session directly (for example, a headless agent running on a server that can display a short code to a human operator).

## Overview

RFC 8628 defines a protocol in which the device (the OAuth client) requests a **device code** and a **user code** from the authorization server, then instructs the user to visit a **verification URI** on a separate device and enter the user code.[^rfc8628]

While the user completes the authorization step, the device client **polls** the authorization server’s token endpoint with the device code until the authorization server returns an access token or an error.[^rfc8628]

## Protocol roles and endpoints

RFC 8628 builds on OAuth 2.0 (RFC 6749) and introduces a new endpoint:

- **Device authorization endpoint**: the client POSTs to this endpoint to obtain the `device_code`, `user_code`, and `verification_uri` values that drive the out-of-band user interaction.[^rfc8628]

The user interacts with the authorization server using a normal browser at the verification URI, authenticates, enters the user code, and approves or denies the request.[^rfc8628]

## Typical flow

A typical device authorization flow includes:[^rfc8628]

1. **Device authorization request**: the client requests codes from the device authorization endpoint.
2. **Device authorization response**: the authorization server returns a `device_code`, `user_code`, and `verification_uri` (and often additional parameters such as `verification_uri_complete`, `expires_in`, and a polling `interval`).
3. **User interaction**: the client shows the verification URI and user code to the user.
4. **Polling**: the client polls the token endpoint with the device code until the user completes the approval step.
5. **Token response**: the authorization server returns an access token (and optionally a refresh token) or an error.

## Security considerations

RFC 8628 discusses several security considerations, including:[^rfc8628]

- **User code brute forcing**: user codes are short by design, so servers need rate limiting and other mitigations.
- **Remote phishing**: attackers may try to trick users into entering codes at a malicious site.
- **Session spying**: the verification URI/code display can be observed in shared or public environments.
- **Non-confidential clients**: device clients often cannot keep secrets, affecting client authentication choices.

## Related specifications

- **OAuth 2.0** (RFC 6749), the base framework that RFC 8628 extends.[^rfc6749]
- **OAuth 2.0 for Native Apps** (RFC 8252), which RFC 8628 notes should be used for capable native apps rather than the device flow.[^rfc8628]

## See also

- [Agent Authorization Profile (AAP) for OAuth 2.0](Agent%20Authorization%20Profile%20(AAP)%20for%20OAuth%202.0.md)
- [DPoP (OAuth 2.0 Demonstrating Proof of Possession)](oauth-dpop-rfc-9449.md)

## References

[^rfc8628]: W. Denniss, J. Bradley, M. Jones, H. Tschofenig, "OAuth 2.0 Device Authorization Grant", RFC 8628, August 2019. https://datatracker.ietf.org/doc/html/rfc8628

[^rfc6749]: D. Hardt, "The OAuth 2.0 Authorization Framework", RFC 6749, October 2012. https://datatracker.ietf.org/doc/html/rfc6749
