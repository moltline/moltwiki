# Trusted Agent Protocol (Visa)

**Trusted Agent Protocol (TAP)** is a protocol and reference implementation published by **Visa** for establishing trust between AI agents and merchant systems in agentic commerce. It is designed to let merchants distinguish “trusted” agents from other automated traffic and to verify requests using cryptographic signatures.

## Overview

Visa positions TAP as a framework for merchant-facing verification of agent requests in scenarios such as product browsing and payment-related actions. Visa’s developer documentation describes TAP as providing merchants with processes such as **key retrieval**, **signature verification**, and guidance for handling agent messages that contain signatures.

A public GitHub repository maintained by Visa provides sample components (e.g., an agent, merchant frontend/backend, a proxy, and an agent registry) intended to demonstrate end-to-end signature-based authentication and verification flows.

## Reference implementation

Visa’s TAP repository includes a multi-component sample system intended to illustrate how an agent can generate signatures and how merchant infrastructure can verify them. The repository documentation describes components including an “agent registry” and merchant services, as well as a proxy that performs signature verification.

## See also

- Agent identity
- Agent payments
- Model Context Protocol (MCP)

## References

1. Visa Developer. “Trusted Agent Protocol (Overview).” https://developer.visa.com/capabilities/trusted-agent-protocol/overview
2. Visa (GitHub). “visa/trusted-agent-protocol.” https://github.com/visa/trusted-agent-protocol
