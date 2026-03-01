---
title: Remote Attestation Procedures (RATS)
---

# Remote Attestation Procedures (RATS)

**Remote ATtestation procedureS (RATS)** is an Internet Engineering Task Force (IETF) effort that standardizes an **architecture**, terminology, and supporting specifications for **remote attestation**: a process where a *verifier* appraises cryptographic **evidence** about a remote *attester*’s state and produces an **attestation result** for a *relying party* to use in a decision. (Architecture: RFC 9334 https://www.rfc-editor.org/rfc/rfc9334.html)

In agentic and tool-using systems, remote attestation is often discussed as a building block for establishing **trust in the execution environment** of an agent, tool server, or gateway (e.g., “only release secrets to an attested runtime”).

## What remote attestation is (and is not)

Remote attestation helps answer questions like:

- “Is this workload running in an expected environment?” (e.g., measured boot, or a specific trusted execution environment)
- “Is the software/firmware configuration what I expect?”
- “Is a cryptographic key bound to that environment being used?”

It does **not** automatically provide:

- authorization (it produces inputs to an authorization/policy decision)
- perfect runtime integrity (it is only as strong as the underlying root of trust, measurement chain, and verifier policy)

## RATS roles and artifacts

RATS frames remote attestation as an interaction among roles (RFC 9334 https://www.rfc-editor.org/rfc/rfc9334.html):

- **Attester**: the entity whose state is being attested; it produces evidence.
- **Verifier**: appraises evidence against policy and reference values, producing an attestation result.
- **Relying Party**: consumes the attestation result to make an authorization or other policy decision.

The architecture distinguishes the messages/artifacts:

- **Evidence**: claims produced by the attester about its state, conveyed to a verifier.
- **Attestation Result**: the verifier’s appraisal output, conveyed to a relying party.

In many deployments, the verifier’s appraisal uses additional inputs that are not produced by the attester, such as **endorsements** (manufacturer or supply-chain statements about the attester) and **reference values** (expected measurements). These concepts are part of the RATS architecture vocabulary (RFC 9334 https://www.rfc-editor.org/rfc/rfc9334.html).

## Freshness and replay resistance

A verifier typically needs a way to determine that evidence is **fresh** (not replayed). RATS treats freshness as an architectural concern (RFC 9334 https://www.rfc-editor.org/rfc/rfc9334.html), and many protocols use challenges (e.g., nonces) or time-based mechanisms depending on the environment.

One concrete example of standardization work around freshness is the LAMPS draft on nonce-based freshness when attestation evidence is used in certificate enrollment flows (https://www.ietf.org/archive/id/draft-ietf-lamps-attestation-freshness-05.html).

## Evidence formats and encapsulation

RATS does not mandate a single wire protocol; instead, it standardizes reusable building blocks.

Commonly referenced pieces of work include:

- **Entity Attestation Token (EAT)**: a claim-set format intended for attestation evidence, typically carried in CBOR/COSE ecosystems. (Status varies by publication; see the RATS WG’s current EAT spec on the IETF datatracker: https://datatracker.ietf.org/doc/draft-ietf-rats-eat/)
- **EAT media types**: registered media types for EAT payloads (RFC 9782 https://www.rfc-editor.org/rfc/rfc9782.html)
- **Conceptual Message Wrapper (CMW)**: a conceptual encapsulation for evidence and attestation results (Internet-Draft: https://datatracker.ietf.org/doc/draft-ietf-rats-msg-wrap/)

## How this shows up in agent/tool ecosystems

Remote attestation is sometimes proposed as a complement to application-layer authorization (e.g., OAuth) when an agent or host must decide whether to:

- release sensitive credentials to a tool server,
- allow an agent to access internal resources,
- or accept tool outputs as coming from an approved execution environment.

In practice, using RATS-style attestation inside an agent stack usually requires:

- a clear threat model (what attacks are mitigated and what are not),
- a verifier service integrated with a policy engine (what constitutes “trusted”),
- and careful handling of privacy/correlation risk (attestation claims can be identifying).

## See also

- [Model Context Protocol (MCP)](Model%20Context%20Protocol%20(MCP).md)
- [Agent Authorization Profile (AAP) for OAuth 2.0](Agent%20Authorization%20Profile%20(AAP)%20for%20OAuth%202.0.md)

## References

- IETF. *Remote ATtestation procedureS (RATS) Architecture* (RFC 9334). RFC Editor. https://www.rfc-editor.org/rfc/rfc9334.html
- IETF RATS Working Group. *RATS WG datatracker page*. https://datatracker.ietf.org/wg/rats/
- IETF. *Nonce-based Freshness for Remote Attestation in Certificate Enrollment* (Internet-Draft). https://www.ietf.org/archive/id/draft-ietf-lamps-attestation-freshness-05.html
- IETF. *The Entity Attestation Token (EAT)* (Internet-Draft). https://datatracker.ietf.org/doc/draft-ietf-rats-eat/
- IETF. *Entity Attestation Token (EAT) Media Types* (RFC 9782). RFC Editor. https://www.rfc-editor.org/rfc/rfc9782.html
- IETF. *RATS Conceptual Messages Wrapper (CMW)* (Internet-Draft). https://datatracker.ietf.org/doc/draft-ietf-rats-msg-wrap/
