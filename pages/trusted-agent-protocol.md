---
title: "Trusted Agent Protocol"
---

# Trusted Agent Protocol

**Trusted Agent Protocol (TAP)** is a specification published by Visa for **agentic commerce** in which merchants and intermediaries (such as CDNs and bot-mitigation providers) can **recognize and verify “approved” AI agents** that interact with merchant web properties or APIs with commerce intent.

Visa describes TAP as a framework for distinguishing commerce-focused agents from malicious automated traffic, and for allowing merchants to validate signed information provided by agents (for example, identity- or payment-related data elements) in browsing and payment flows.<ref name="visa-overview">https://developer.visa.com/capabilities/trusted-agent-protocol/overview</ref>

## Overview

TAP is aimed at scenarios where an agent is **initially unknown to a merchant**, and where the merchant needs a scalable way to decide whether to allow, limit, or tailor interactions from automated clients without relying on mechanisms such as IP allowlists or user-agent strings.<ref name="visa-spec">https://developer.visa.com/capabilities/trusted-agent-protocol/trusted-agent-protocol-specifications</ref>

Visa’s merchant specification describes two primary interaction phases:

- **Browsing interactions**, where an agent initiated by a consumer with commerce intent seeks product details, availability, taxes, and shipping information.
- **Payment interactions**, where an agent provides information necessary to complete a purchase or gain paid access to a merchant resource.<ref name="visa-spec" />

## Trust model

Visa’s specification describes a trust model comprised of **three distinct signatures**:

1. **Agent recognition signature** in a message header, intended to let a merchant verify that a request originates from a trusted agent and to help prevent replay/relay.
2. **Linked and signed consumer/device identity** in the message body, intended to help a merchant determine whether the consumer is known to the merchant (for example via an account or prior interactions).
3. **Linked and signed payment container** in the message body, intended to provide payment-credential-related information needed to complete or complement a purchase, depending on the merchant integration mechanism.<ref name="visa-spec" />

## Cryptographic mechanisms

The merchant specification states that the agent recognition signature is based on **HTTP Message Signatures** as defined in **RFC 9421**, using structured fields such as `Signature-Input` and `Signature` to convey signature metadata and the signature value.<ref name="visa-spec" /><ref name="rfc9421">https://datatracker.ietf.org/doc/html/rfc9421</ref>

## Implementations

Visa provides a public GitHub repository with sample code demonstrating TAP components (including an agent, merchant front end and back end, a proxy layer, and an agent registry).<ref name="visa-github">https://github.com/visa/trusted-agent-protocol</ref>

## See also

- [[Agentic commerce]]
- [[Agent payments]]

## References

<references />
