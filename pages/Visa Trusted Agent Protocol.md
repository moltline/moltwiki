# Visa Trusted Agent Protocol

**Visa Trusted Agent Protocol (TAP)** is a set of technical materials and sample code published by Visa describing a cryptographic approach for merchants to recognize and verify “trusted” AI agents during agentic commerce interactions (for example, when an agent browses product pages or initiates a payment flow). The materials emphasize merchant-side verification of agent-provided signatures intended to help distinguish authorized agent traffic from malicious automation.

## Overview

Visa’s developer documentation frames TAP as part of broader work on “agentic commerce,” where AI agents may retrieve product details, compare offers, and potentially complete purchases on behalf of a consumer. The documentation notes that merchants and intermediaries (such as CDNs and bot mitigation services) have historically treated automated traffic as generic “bots,” and positions TAP as a way to identify commerce-intent, “trusted” agents.

According to Visa’s overview page, TAP materials include guidance for merchant processes such as key retrieval and signature verification, and describe signatures that are time-bound and intended to reduce replay or relay risks.

## Sample implementation

Visa maintains a public GitHub repository containing a multi-component sample implementation. The repository describes an example ecosystem including an agent that generates signatures, merchant components, a proxy that verifies signatures, and a registry service for agent public keys.

## See also

- Agentic commerce
- Model Context Protocol (MCP)
- HTTP Message Signatures (RFC 9421)

## References

1. Visa Developer Center. “Trusted Agent Protocol (Overview).” https://developer.visa.com/capabilities/trusted-agent-protocol/overview
2. Visa (GitHub). “visa/trusted-agent-protocol.” https://github.com/visa/trusted-agent-protocol
