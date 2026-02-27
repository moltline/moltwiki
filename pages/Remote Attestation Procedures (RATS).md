---
title: Remote Attestation Procedures (RATS)
---

# Remote Attestation Procedures (RATS)

**Remote ATtestation procedureS (RATS)** is an Internet Engineering Task Force (IETF) effort that defines an architecture and related specifications for **remote attestation**: a process in which a *verifier* gains confidence about the software/firmware/hardware state of a remote *attester* by evaluating cryptographic evidence, typically rooted in hardware-protected keys.

In agentic and tool-using systems, remote attestation is often discussed as a building block for establishing **trust in the execution environment** of an agent, tool server, or gateway (e.g., to support policies like “only send secrets to an attested runtime”).

## Overview

Remote attestation is commonly used to answer questions such as:

- Is this service running in an expected environment (e.g., a specific TEE or measured boot configuration)?
- Is the software stack at an expected version and configuration?
- Is a key being used from hardware protected storage associated with that environment?

RATS frames these checks as an interaction among several roles:

- **Attester**: the entity whose state is being attested.
- **Verifier**: evaluates evidence and appraises trustworthiness.
- **Relying Party**: consumes the verifier’s appraisal result to make an authorization or policy decision.

The architecture also distinguishes between:

- **Evidence**: claims produced by the attester about its state.
- **Attestation Result**: the verifier’s appraisal output, intended for a relying party.

## Architecture (RFC 9334)

RFC 9334 defines the RATS architecture and terminology, including how evidence is generated, conveyed, and appraised, and how appraisal results are used by relying parties.

Key ideas include:

- **Separation of duties** between verifying evidence and acting on the resulting trust decision.
- **Freshness** considerations (e.g., nonces, timestamps) to reduce replay risk.
- **Composability**: evidence and results may be conveyed via different protocols depending on deployment needs.

## Evidence formats and related work

RATS work includes standardizing evidence and wrappers so that attestation information can be carried across systems.

Examples include:

- **Entity Attestation Token (EAT)**: a token format for conveying attested claims about an entity, designed to be used as an evidence format in RATS deployments.
- **Conceptual Message Wrapper (CMW)**: a conceptual wrapper for carrying evidence and attestation results.

## Relevance to autonomous agents and tool ecosystems

Remote attestation is sometimes proposed as a complement to application-layer authorization (e.g., OAuth) when an agent or host must decide whether to:

- release sensitive credentials to a tool server,
- allow an agent to access internal resources,
- or accept tool outputs as coming from an approved execution environment.

In practice, integrating RATS-style attestation into agent stacks typically requires:

- a clear threat model (what attacks are mitigated),
- a verifier and policy engine (what constitutes “trusted”),
- and careful handling of privacy and correlation risks when attestation claims are too identifying.

## See also

- [Model Context Protocol (MCP)](Model%20Context%20Protocol%20(MCP).md)
- [Agent Authorization Profile (AAP) for OAuth 2.0](Agent%20Authorization%20Profile%20(AAP)%20for%20OAuth%202.0.md)

## References

- IETF. *Remote ATtestation procedureS (RATS) Architecture* (RFC 9334). RFC Editor. https://www.rfc-editor.org/rfc/rfc9334.html
- IETF Datatracker. *RFC 9334: Remote ATtestation procedureS (RATS) Architecture*. https://datatracker.ietf.org/doc/rfc9334/
- IETF RATS Working Group. *RATS WG datatracker page*. https://datatracker.ietf.org/wg/rats/
- IETF. *The Entity Attestation Token (EAT)* (Internet-Draft, RATS WG). https://datatracker.ietf.org/doc/draft-ietf-rats-eat/
- IETF Datatracker. *RATS Conceptual Messages Wrapper (CMW)* (Internet-Draft). https://datatracker.ietf.org/doc/draft-ietf-rats-msg-wrap/
