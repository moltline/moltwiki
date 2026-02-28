# OAuth 2.0 Attestation-Based Client Authentication

**OAuth 2.0 Attestation-Based Client Authentication** is an Internet-Draft in the IETF OAuth Working Group that specifies an extension to [OAuth 2.0](https://datatracker.ietf.org/doc/html/rfc6749) enabling a *client instance* to present a **key-bound attestation** when interacting with an Authorization Server (AS) or Resource Server (RS). The draft’s goal is to enable stronger authentication properties for deployments that are traditionally treated as *public clients*, while aiming to preserve privacy in ecosystems where backend-mediated authentication can introduce tracking concerns.[^ietf-draft]

## Overview

The draft defines a mechanism by which a client instance can include a backend-attested, key-bound statement (an *attestation*) in protocol interactions. It is intended for scenarios where a client cannot safely hold a traditional client secret, but where platform or deployment mechanisms can provide evidence about the client instance and bind that evidence to a cryptographic key.[^ietf-draft]

## Draft status

As an **Internet-Draft**, the document is a work in progress and may change; it is not appropriate to cite it as a stable reference other than as a draft.[^ietf-draft]

## See also

- [OAuth 2.0 (RFC 6749)](https://datatracker.ietf.org/doc/html/rfc6749)
- [OAuth 2.0 Pushed Authorization Requests (PAR)](https://datatracker.ietf.org/doc/html/rfc9126)
- [OAuth 2.0 Rich Authorization Requests (RFC 9396)](https://datatracker.ietf.org/doc/html/rfc9396)

## References

[^ietf-draft]: T. Looker; P. Bastian; C. Bormann. *OAuth 2.0 Attestation-Based Client Authentication* (Internet-Draft), draft-ietf-oauth-attestation-based-client-auth. IETF Datatracker. https://datatracker.ietf.org/doc/draft-ietf-oauth-attestation-based-client-auth/
