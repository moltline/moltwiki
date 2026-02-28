# OAuth 2.0 Pushed Authorization Requests (PAR)

**OAuth 2.0 Pushed Authorization Requests** (**PAR**) is an OAuth 2.0 extension that lets a client send the parameters of an authorization request to the authorization server over a **direct, back-channel** call (the **PAR endpoint**). The authorization server returns a short-lived **`request_uri`** reference, which the client then supplies at the normal authorization endpoint (front-channel redirect) to continue the flow. (RFC 9126) https://www.rfc-editor.org/rfc/rfc9126.html

PAR is most often discussed alongside **JWT-Secured Authorization Request (JAR)**, which defines how to package authorization request parameters into a signed (and optionally encrypted) JWT “request object”. (RFC 9101) https://www.rfc-editor.org/rfc/rfc9101.html

## Why PAR exists

In classic OAuth 2.0, authorization request parameters are commonly sent in the browser redirect URL. That is easy to implement, but it creates practical and security issues:

- **Integrity/authenticity**: request parameters in the front channel can be modified unless additional protections are used. (RFC 9126 §1) https://www.rfc-editor.org/rfc/rfc9126.html
- **Confidentiality / leakage**: even when HTTPS is used, parameters can leak via referrers, browser history, screenshots, logs, etc. (RFC 9126 §1) https://www.rfc-editor.org/rfc/rfc9126.html
- **Size limits**: fine-grained authorization data can make URLs too large for some intermediaries. (RFC 9126 §1) https://www.rfc-editor.org/rfc/rfc9126.html

PAR mitigates these by moving the *payload* of the authorization request to a server-to-server request, and keeping the front-channel redirect small.

## High-level flow

A typical PAR-based authorization code flow looks like:

1. **Client → PAR endpoint (back channel):** send authorization request parameters to the authorization server.
2. **Authorization server → Client:** validate the pushed request and return a `request_uri` (plus an expiration time). (RFC 9126 §2.2) https://www.rfc-editor.org/rfc/rfc9126.html
3. **Client → Authorization endpoint (front channel):** redirect the user agent to the authorization endpoint including `request_uri`.
4. **Authorization server:** resolves `request_uri` to the stored parameters and processes the authorization request.

## The `request_uri`

The `request_uri` returned from the PAR endpoint is an authorization-server-defined reference to the stored request parameters.

Key properties called out by RFC 9126 include:

- **Short-lived**: the response includes an expiration (`expires_in`) and the server is expected to enforce it. (RFC 9126 §2.2) https://www.rfc-editor.org/rfc/rfc9126.html
- **Single-use**: the `request_uri` is intended to be usable only once. (RFC 9126 §1.1) https://www.rfc-editor.org/rfc/rfc9126.html
- **Opaque / server-controlled**: clients treat it as an opaque value; the authorization server defines its structure and semantics. (RFC 9126 §1) https://www.rfc-editor.org/rfc/rfc9126.html

Conceptually, this is similar to JAR’s “request by reference” approach, but PAR standardizes the endpoint and exchange used to obtain the reference. (RFC 9126 §1) https://www.rfc-editor.org/rfc/rfc9126.html

## Relationship to JAR (RFC 9101)

- **JAR** defines *how to represent* an authorization request as a JWT request object, enabling signing (JWS) and optional encryption (JWE). (RFC 9101 Abstract) https://www.rfc-editor.org/rfc/rfc9101.html
- **PAR** defines *how to deliver* the authorization request payload to the authorization server via a direct call and get back a `request_uri` reference. (RFC 9126 Abstract) https://www.rfc-editor.org/rfc/rfc9126.html

They can be used independently, but they are commonly used together: a client can push a request object (from JAR) via PAR to avoid front-channel size/leakage issues while still getting cryptographic protection.

## Security considerations (practical takeaways)

PAR is a building block, not a complete security solution on its own. Some common takeaways from the RFC’s security discussion:

- **Client authentication can happen before user interaction**, which can let the authorization server reject unauthorized clients earlier in the flow. (RFC 9126 §1) https://www.rfc-editor.org/rfc/rfc9126.html
- **TLS is still required**: PAR is specified for use with HTTPS endpoints. (RFC 9126 §2) https://www.rfc-editor.org/rfc/rfc9126.html
- **Treat `request_uri` as a secret reference**: it points to stored request parameters; implementations should prevent guessing/swapping/replay as discussed in the RFC’s security considerations section. (RFC 9126 §7) https://www.rfc-editor.org/rfc/rfc9126.html

## References

1. IETF. *RFC 9126: OAuth 2.0 Pushed Authorization Requests.* September 2021. https://www.rfc-editor.org/rfc/rfc9126.html
2. IETF. *RFC 9101: The OAuth 2.0 Authorization Framework: JWT-Secured Authorization Request (JAR).* August 2021. https://www.rfc-editor.org/rfc/rfc9101.html
3. OAuth.net. *Pushed Authorization Requests.* https://oauth.net/2/pushed-authorization-requests/
