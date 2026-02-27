# Grant Negotiation and Authorization Protocol (GNAP)

The **Grant Negotiation and Authorization Protocol (GNAP)** is an Internet Engineering Task Force (IETF) standards-track protocol for delegating authorization to client software and conveying the results of that delegation (such as access tokens and related artifacts) to the client. GNAP is designed to support fine-grained, transaction-scoped authorization and multiple interaction patterns beyond the browser-redirect flows commonly associated with OAuth 2.0.

GNAP was developed in the IETF **GNAP** working group, which has concluded after publication of its planned work items.

## Overview

GNAP defines a protocol between a **client instance** and an **authorization server (AS)** for requesting and obtaining authorization to access one or more **resource servers (RSs)**. The protocol is intended to be flexible about how end-user interaction occurs, including:

- redirect-based interaction
- user-code interaction
- asynchronous authorization (where the client polls for completion)
- software-only authorization flows

GNAP also defines mechanisms for returning **subject information** to the client, in addition to (or instead of) access tokens.

## Relationship to OAuth 2.0 and OpenID Connect

GNAP is positioned as an alternative delegation protocol that seeks to expand on use cases supported by OAuth 2.0 and OpenID Connect, including more explicit modeling of roles and interactions, finer-grained access, and reduced dependence on browser-based redirection as the primary coordination mechanism.

## Key concepts

### Roles

GNAP describes interactions among multiple parties involved in authorization, including:

- **Client** (client instance): the software requesting delegated access
- **Authorization server (AS)**: the service that determines whether and how access is granted
- **Resource server (RS)**: the service hosting protected resources/API endpoints
- **End user / authorizing party**: the party whose authorization may be required

### Grant request and response

A client requests access by sending a **grant request** to an AS. A successful response can include:

- one or more access tokens
- continuation information for multi-step or asynchronous flows
- interaction instructions for involving the end user
- subject information and/or assertions

### Interaction modes

GNAP standardizes several interaction modes that an AS can use to direct the client on how to involve an end user, including redirection and user-code based approaches.

### Securing requests and proof-of-possession

GNAP includes mechanisms for securing requests from the client instance and for binding tokens to cryptographic keys (proof-of-possession). The protocol supports multiple approaches, including **HTTP Message Signatures**.

## Extensions

The GNAP ecosystem includes extensions that define interoperable methods for RS–AS connections.

- **RFC 9767** defines methods for resource servers to connect with authorization servers in an interoperable fashion.

## See also

- [OAuth 2.0 Extension On-Behalf-Of User Authorization for AI Agents](OAuth%202.0%20Extension%20On-Behalf-Of%20User%20Authorization%20for%20AI%20Agents.md)
- [HTTP Message Signatures (RFC 9421)](HTTP%20Message%20Signatures%20(RFC%209421).md)
- [Model Context Protocol (MCP) Authorization](Model%20Context%20Protocol%20(MCP)%20Authorization.md)

## References

- J. Richer; F. Imbault. *Grant Negotiation and Authorization Protocol (GNAP).* IETF RFC 9635 (Standards Track), October 2024. https://www.rfc-editor.org/rfc/rfc9635
- J. Richer; F. Imbault. *Grant Negotiation and Authorization Protocol Resource Server Connections.* IETF RFC 9767 (Standards Track), April 2025. https://www.rfc-editor.org/rfc/rfc9767.html
- IETF Datatracker. *Grant Negotiation and Authorization Protocol (gnap) Working Group (concluded).* https://datatracker.ietf.org/wg/gnap/about/
