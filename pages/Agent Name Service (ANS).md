# Agent Name Service (ANS)

**Agent Name Service (ANS)** is a proposed architecture for discovering AI agents via DNS-inspired names and resolving them to verifiable identity and capability metadata. ANS is described as a protocol-agnostic agent registry design that can advertise how to reach an agent over multiple emerging agent communication protocols (such as A2A and MCP), while binding registry entries to public-key credentials for authenticity.[1]

ANS is published as an Internet-Draft in the IETF Datatracker. As an Internet-Draft, it is a work in progress and may change, be replaced, or expire.[1]

## Overview

The ANS draft proposes an agent directory service intended to support:

- **Discovery**: resolving a human-readable, DNS-like agent name to a structured record describing the agent and its endpoints.[1]
- **Verifiable identity and trust**: associating registry entries with **PKI** credentials (e.g., X.509 certificates) to help prevent impersonation and enable authenticated resolution.[1]
- **Lifecycle management**: registration and renewal mechanisms for maintaining current records over time.[1]
- **Protocol interoperability**: a **protocol adapter layer** intended to map a common registry record format into protocol-specific metadata for multiple agent protocols.[1]

## Architecture

The draft describes a registry architecture with roles including a **requesting agent** (or operator) submitting registration requests, an **agent registry** storing identity and capability data, and a **registration authority** and **certificate authority** participating in credential issuance and validation.[1]

The design also includes a **Protocol Adapter Layer** that can expose protocol-specific details for different communication standards.[1]

## Relationship to other agent standards

ANS is positioned as complementary to emerging agent communication and tool-integration protocols. The draft explicitly references multiple protocols and describes adapters for them, including:

- **Agent2Agent (A2A) Protocol**[1]
- **Model Context Protocol (MCP)**[1]
- **Agent Communication Protocol (ACP)**[1]

## Security considerations

The draft includes a security considerations section and discusses threats such as agent impersonation, registry poisoning, and man-in-the-middle attacks, with mitigations based on authenticated resolution and PKI-backed identity binding.[1]

## References

1. IETF Datatracker. "Agent Name Service (ANS): A Universal Directory for Secure AI Agent Discovery and Interoperability" (Internet-Draft draft-narajala-ans-00). https://datatracker.ietf.org/doc/html/draft-narajala-ans-00 (accessed 2026-02-27).
