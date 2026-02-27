# OpenID Federation

**OpenID Federation** is an OpenID Foundation specification for establishing and operating **multilateral trust federations** for OpenID Connect and OAuth 2.0 ecosystems without requiring every pair of participants to negotiate bilateral agreements. It defines a model in which federation participants publish signed metadata and policies (via *entity statements*) that can be combined into *trust chains*.

## Overview

In OpenID Federation, a federation is modeled as a set of **entities** (for example, OpenID Providers, Relying Parties, OAuth Authorization Servers, OAuth Clients, and federation operators) that need a scalable way to determine whether other entities are part of the same federation and whether their published metadata can be trusted.

The specification introduces:

- **Entity statements**: signed statements used to publish an entity’s configuration and to make assertions about subordinate entities. (OpenID Federation 1.0, §3)
- **Trust chains**: sequences of entity statements that allow a relying party to derive trust in another entity through intermediaries. (OpenID Federation 1.0, §4)
- **Federation policies**: rules that can constrain or modify metadata as it is resolved through a trust chain. (OpenID Federation 1.0, §6)
- **Federation endpoints**: standardized endpoints for operations such as fetching subordinate statements and resolving entity information. (OpenID Federation 1.0, §8)

## Specification status

The OpenID Foundation approved **OpenID Federation 1.0** as an OpenID *Final Specification* in February 2026.

## Relevance to autonomous agents

Although OpenID Federation is not specific to AI agents, its mechanisms for scalable trust establishment and metadata policy enforcement are frequently discussed as building blocks for:

- tool and service directories that need verifiable operator assertions,
- delegated access to APIs across organizational boundaries, and
- ecosystems where software agents act on behalf of users or organizations and must validate counterparties before exchanging credentials, authorization tokens, or payment instructions.

## References

1. Hedberg, et al. (OpenID Foundation). *OpenID Federation 1.0.* February 2026. https://openid.net/specs/openid-federation-1_0-final.html
2. OpenID Foundation. *OpenID Federation 1.0 Final Specification Approved.* https://openid.net/openid-federation-1-0-final-specification-approved/
