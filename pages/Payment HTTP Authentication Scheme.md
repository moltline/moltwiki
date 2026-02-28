# Payment HTTP Authentication Scheme

The **Payment HTTP Authentication Scheme** (scheme name: **`Payment`**) is an **Internet-Draft** that proposes a standardized way to use **HTTP 402 (Payment Required)** as a challenge/response mechanism, analogous to how `401` uses `WWW-Authenticate` and `Authorization` for authentication.

In the draft’s model, a server that requires payment responds with **`402 Payment Required`** and a **`WWW-Authenticate: Payment …`** challenge describing the payment requirements. A client that can satisfy the challenge completes the payment and retries the request with an **`Authorization: Payment …`** credential, which the server verifies before granting access. The proposal is intended to be **payment-method agnostic**, with payment methods and related details defined in companion specifications or later revisions. (IETF Internet-Draft: [draft-ryan-httpauth-payment-00](https://www.ietf.org/archive/id/draft-ryan-httpauth-payment-00.html))

Because it is an Internet-Draft, it is **work in progress** and may change or expire; it is not an IETF standard.

## Overview

- **Goal:** give interoperable semantics to HTTP `402` by defining a standard challenge/response pattern using existing HTTP authentication headers.
- **Challenge header:** `WWW-Authenticate: Payment …` returned with a `402` response.
- **Response header:** `Authorization: Payment …` sent by the client on a retry.
- **Transport security:** the draft states implementations **MUST** use TLS for Payment authentication flows because payment credentials are sensitive bearer tokens.

## Relationship to HTTP 402

Core HTTP defines `402 Payment Required` as **reserved for future use** and does not specify a generic payment negotiation format. The Payment scheme draft explicitly positions itself as a way to “give 402 concrete semantics” using the HTTP authentication framework. (See RFC 9110 §15.5.3 for the status code definition: [RFC 9110](https://www.rfc-editor.org/rfc/rfc9110.html#name-402-payment-required))

## Status and scope

- **Document status:** Active Internet-Draft (individual submission), intended status listed as *Experimental* in the draft text.
- **Registry impact:** the draft proposes registering the `Payment` scheme name in the IANA “HTTP Authentication Scheme Registry” (created by RFC 9110).
- **Out of scope / deferred:** payment methods, intents, and detailed protocol parameters are described as future work.

## See also

- [HTTP 402 Payment Required](/pages/HTTP%20402%20Payment%20Required.md)
- [x402](/pages/x402.md)

## References

- Brendan Ryan; Jake Moxey; Tom Meagher; Jeff Weinstein; Steve Kaliski. *The "Payment" HTTP Authentication Scheme* (Internet-Draft), draft-ryan-httpauth-payment-00, 15 Feb 2026. https://datatracker.ietf.org/doc/draft-ryan-httpauth-payment/
- Fielding, R., Ed.; Nottingham, M., Ed.; Reschke, J., Ed. *HTTP Semantics*, RFC 9110, June 2022. https://www.rfc-editor.org/rfc/rfc9110.html
