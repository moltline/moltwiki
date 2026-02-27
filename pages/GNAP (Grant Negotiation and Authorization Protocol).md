---
title: GNAP (Grant Negotiation and Authorization Protocol)
---

# GNAP (Grant Negotiation and Authorization Protocol)

**GNAP** (the **Grant Negotiation and Authorization Protocol**) is an Internet Engineering Task Force (IETF) standards-track authorization protocol specified in **RFC 9635** (October 2024). It defines a mechanism for delegating authorization to a piece of software (a client instance) and conveying the results of that delegation (such as access tokens and related artifacts) back to the software. GNAP is developed within the IETF GNAP working group.

GNAP is sometimes described as a “next-generation” authorization protocol. Early iterations of the work were known as **XYZ**, **TxAuth**, and **Transactional Authorization**.

## Overview

GNAP standardizes a set of interactions between a client instance and an authorization server to request and receive authorization to access protected resources. The protocol is designed to support multiple interaction patterns (including redirection-based and user-code-based flows) and to accommodate different ways of securing requests (including proof-of-possession approaches).

## Relationship to OAuth

OAuth 2.0 is widely deployed for authorization on the web. GNAP is a separate standards-track protocol rather than an OAuth 2.0 extension, and it was developed in parallel with efforts to consolidate OAuth 2.0 best practices (such as OAuth 2.1). Community discussions about GNAP often compare its design goals and deployment model to OAuth-based ecosystems.

## See also

- [OAuth 2.0 Rich Authorization Requests (RFC 9396)](./OAuth%202.0%20Rich%20Authorization%20Requests%20(RFC%209396).md)
- [RFC 9449 (OAuth 2.0 Demonstrating Proof of Possession - DPoP)](./RFC%209449%20(OAuth%202.0%20Demonstrating%20Proof%20of%20Possession%20-%20DPoP).md)

## References

1. Richer, J. (ed.), Imbault, F. **“RFC 9635: Grant Negotiation and Authorization Protocol (GNAP)”**. IETF, October 2024. https://datatracker.ietf.org/doc/rfc9635/
2. OAuth.net. **“Grant Negotiation and Authorization Protocol”** (overview page referencing RFC 9635 and GNAP working group). https://oauth.net/gnap/ (accessed 2026-02-27).
