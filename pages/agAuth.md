# agAuth

**agAuth** is a draft, open specification for cryptographic identity and authentication for autonomous AI agents. The project describes a model in which an agent carries a persistent keypair and presents signed, scoped assertions to services at runtime, rather than relying on forwarding end-user credentials to each service the agent uses.

## Overview

The agAuth repository frames the specification as an “identity layer” for agents, analogous to OAuth for humans, intended to support portable agent identity across services. It introduces concepts including an agent identifier ("agID"), a long-lived Ed25519 keypair ("Soul-Key"), and a signed, time-bounded token ("agToken") used when authenticating to services.

The repository also positions agAuth as complementary to the project's "Agentic Commerce Protocol" (ACP), describing agAuth as the identity layer and ACP as a transport layer for agent-to-agent communication.

## Concepts

The agAuth README describes several named primitives:

- **agID**: a globally unique agent identifier.
- **Soul-Key**: an Ed25519 keypair representing the agent’s cryptographic identity.
- **agToken**: a signed assertion containing identity and authorization scope information, intended to be presented at runtime.
- **Issuer node**: user-controlled infrastructure that issues keys and tokens.

## See also

- [[Agent identity]]
- [[Agentic Commerce Protocol (ACP)]]
- [[x402]]

## References

1. Architect-SIS. "agAuth — Agent Authentication Standard" (repository README). GitHub. https://github.com/Architect-SIS/agauth (accessed 2026-02-27).
