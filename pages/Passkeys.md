# Passkeys

A **passkey** is a passwordless authentication credential based on [FIDO](https://fidoalliance.org/fido2/) standards. In typical deployments, a passkey enables a user to sign in to a website or application by approving an authentication prompt using the same local method used to unlock a device (for example, biometrics or a device PIN), rather than typing a password.[^fido-passkeys]

Passkeys are commonly implemented using the **FIDO2** family of standards, including the W3C **Web Authentication (WebAuthn)** API for browsers and the FIDO **Client to Authenticator Protocol (CTAP)** for communication with authenticators.[^fido-passkeys][^webauthn]

## Overview

Passkeys are typically based on public-key cryptography:

- A **private key** is held by (or protected by) an authenticator associated with the user.
- A corresponding **public key** is stored by the relying party (the service being accessed).

When authenticating, the user agent and authenticator produce a cryptographic assertion that can be verified by the relying party, rather than transmitting a reusable secret such as a password.[^passkey-central-intro]

## Relationship to WebAuthn and FIDO2

Passkeys are closely associated with the WebAuthn ecosystem:

- The WebAuthn specification defines an API for creating and using public key-based credentials for strongly authenticating users, including registration and authentication "ceremonies" between a relying party, user agent, and authenticator.[^webauthn]
- FIDO Alliance materials describe passkeys as FIDO cryptographic credentials intended to replace passwords and reduce susceptibility to phishing and credential stuffing.[^fido-passkeys]
- The FIDO Client to Authenticator Protocol (CTAP) specifies an application-layer protocol for communication between a client/platform and a roaming authenticator, and is part of the broader FIDO2 project alongside WebAuthn.[^ctap]

## Single-device and multi-device passkeys

Some sources distinguish between passkeys that are bound to a particular authenticator and passkeys that can be synchronized across a user's devices:

- **Device-bound passkeys** never leave a single device.
- **Synced passkeys** can be synchronized across a user's devices via a cloud service.

FIDO Alliance materials use this synced vs device-bound terminology when delineation is required.[^fido-passkeys]

## Security properties and deployment considerations

- **Phishing resistance**: Because authentication uses a scoped public-key credential rather than a reusable shared secret, passkeys are generally considered phishing-resistant when implemented with WebAuthn/FIDO2.
- **Origin / relying party scoping**: WebAuthn credentials are scoped so that they can only be accessed by origins belonging to the relying party, helping limit credential use to the intended site.[^webauthn]
- **User presence / verification**: Authenticators can incorporate evidence of user interaction (for example, a user gesture) and may support user verification (for example, a PIN), depending on authenticator capabilities.[^ctap]

CISA guidance on phishing-resistant MFA commonly includes FIDO-based authentication (for example, WebAuthn/FIDO2) as a recommended approach for reducing phishing risk.[^cisa-phishing-resistant-mfa]

## Use in agentic systems

In systems that support autonomous or semi-autonomous agents, passkeys can be relevant where a user must authenticate to a web service, authorize a payment, or approve sensitive actions.

For example, an agent operating through a browser automation layer may still rely on WebAuthn-capable authenticators for high-assurance user presence and approval, depending on the service and platform.

## See also

- [[Web Authentication (WebAuthn)]]
- [[Secure Payment Confirmation (W3C)]]

## References

[^fido-passkeys]: FIDO Alliance. "FIDO Passkeys: Passwordless Authentication". https://fidoalliance.org/passkeys/
[^passkey-central-intro]: Passkey Central. "Introduction to Passkeys". https://www.passkeycentral.org/introduction-to-passkeys/
[^webauthn]: W3C Web Authentication Working Group. "Web Authentication: An API for accessing Public Key Credentials". https://w3c.github.io/webauthn/
[^ctap]: FIDO Alliance. "Client to Authenticator Protocol (CTAP)" (CTAP 2.2 review draft). https://fidoalliance.org/specs/fido-v2.2-rd-20230321/fido-client-to-authenticator-protocol-v2.2-rd-20230321.html
[^cisa-phishing-resistant-mfa]: CISA. "Implementing Phishing-Resistant MFA" (fact sheet). https://www.cisa.gov/sites/default/files/publications/fact-sheet-implementing-phishing-resistant-mfa-508c.pdf
