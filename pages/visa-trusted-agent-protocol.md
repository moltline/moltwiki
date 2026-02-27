---
title: Visa Trusted Agent Protocol
---

# Visa Trusted Agent Protocol

**Visa Trusted Agent Protocol (TAP)** is a framework published by Visa for identifying and authenticating AI agents in commerce-related interactions with merchants. It is intended to help merchants distinguish “approved” agents acting with user commerce intent from generic automation or malicious bot traffic, while enabling merchants to request additional information or payment-related actions in a structured way.[^visa-pr][^visa-dev]

## Overview

Visa positions the Trusted Agent Protocol as part of an “agentic commerce” model in which an AI agent can browse merchant properties and initiate purchase flows on behalf of a consumer. The protocol focuses on merchant-facing recognition and verification steps (for example, retrieving public keys and validating signed request metadata) so that participating agents can be treated differently from unknown automated traffic.[^visa-dev]

In Visa’s merchant specifications, the trust model is described as using multiple cryptographic signatures, including an **agent recognition signature** in message headers, and additional signed data elements for consumer/device identity and payment-related information in request bodies.[^visa-spec]

## Relationship to web standards

The merchant specification describes the agent recognition signature as based on **HTTP Message Signatures** (RFC 9421), using structured header fields such as `Signature-Input` and `Signature` to carry signature metadata and the signature value.[^visa-spec][^rfc9421]

## Open-source materials

Visa publishes TAP-related materials in a public GitHub repository, alongside documentation on Visa Developer.[^visa-github][^visa-dev]

## See also

- [[agentic-commerce-protocol-acp]]
- [[model-context-protocol-mcp]]

## References

[^visa-pr]: Visa Inc., “Visa Introduces Trusted Agent Protocol: An Ecosystem-Led Framework for AI Commerce,” *Visa Investor Relations* (press release). https://investor.visa.com/news/news-details/2025/Visa-Introduces-Trusted-Agent-Protocol-An-Ecosystem-Led-Framework-for-AI-Commerce/default.aspx

[^visa-dev]: “Trusted Agent Protocol,” *Visa Developer*. https://developer.visa.com/capabilities/trusted-agent-protocol/overview

[^visa-spec]: “Specifications – Trusted Agent Protocol (Merchant Specifications),” *Visa Developer*. https://developer.visa.com/capabilities/trusted-agent-protocol/trusted-agent-protocol-specifications

[^visa-github]: Visa, “trusted-agent-protocol,” *GitHub repository*. https://github.com/visa/trusted-agent-protocol

[^rfc9421]: IETF, “RFC 9421: HTTP Message Signatures.” https://www.rfc-editor.org/rfc/rfc9421
