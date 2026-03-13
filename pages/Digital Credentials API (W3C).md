# Digital Credentials API (W3C)

## Summary

**Digital Credentials API** is a draft W3C specification that proposes a browser-mediated API for requesting and issuing “real-world” digital credentials (e.g., mobile driver’s licenses) on the Web. The design aims to give user agents more ability to provide transparency, user control, and risk mitigation than ad-hoc approaches such as custom URL schemes.

## Why it matters

- **Browser mediation**: enables consistent user interaction and security/privacy checks around credential presentation and issuance.
- **Interoperability**: provides a standardized surface for wallets, issuers, and verifiers instead of app-specific integrations.
- **Ecosystem bridge**: intended to integrate with existing credential formats and protocols (e.g., ISO mdoc, W3C Verifiable Credentials, OpenID4VP / OpenID4VCI).

## Status

This work is being developed in the W3C Federated Identity community (w3c-fedid) and published as a W3C Editor’s Draft / Working Draft.

## Key concepts

- **Verifier / relying party**: a website requesting a credential presentation.
- **Issuer**: a website initiating issuance of a credential to a user’s wallet.
- **Wallet / holder**: software that stores credentials and responds to requests.
- **Request transparency, response opacity**: the API is intended to allow user-agent inspection of requests for risk analysis while assuming responses may be encrypted to limit exposure of sensitive data.

## References

- W3C TR draft: Digital Credentials API — https://www.w3.org/TR/digital-credentials/
- Repository (spec + explainer): https://github.com/w3c-fedid/digital-credentials
- Explainer (raw): https://raw.githubusercontent.com/w3c-fedid/digital-credentials/main/explainer.md
- Background: “Concerns with custom schemes for identity presentment” (raw) — https://raw.githubusercontent.com/w3c-fedid/digital-credentials/main/custom-schemes.md
