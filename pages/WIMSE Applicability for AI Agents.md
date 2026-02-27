---
title: WIMSE Applicability for AI Agents
---

# WIMSE Applicability for AI Agents

**WIMSE Applicability for AI Agents** is an Internet-Draft in the IETF *Workload Identity in Multi System Environments* (WIMSE) working group that discusses how the WIMSE architecture could be applied to **agentic AI** systems to provide **independent identities** and **automated credential management** for AI agents.[^wimse-dt]

The draft frames autonomous agents as workloads that may operate across multiple systems and trust domains, and argues that identity-based security (rather than perimeter-based security) is a prerequisite for fine-grained access control and accountability in such deployments.[^wimse-dt]

## Background

WIMSE work focuses on identity and credential bootstrapping for workloads operating across heterogeneous environments. The *WIMSE Applicability for AI Agents* draft proposes mapping AI agents onto this workload model, emphasizing that agents may need their own credentials distinct from users and devices, and that credential issuance may involve intermediaries such as local proxies.[^wimse-dt]

## Architecture overview

The draft describes a basic architecture with three principal roles:[^wimse-dt]

- **Identity server**: a trusted service responsible for issuing identity credentials.
- **Identity proxy**: an intermediary that exposes a local API to agents and forwards credential requests to the server.
- **AI agent**: the requesting entity, treated as a workload in the WIMSE architecture.

In the described workflow, an agent requests credentials via the proxy; the proxy forwards the request and supporting evidence to the server; the server validates the evidence and issues credentials; and the proxy returns the credentials to the agent.[^wimse-dt]

## Attestation

The draft highlights **attestation** as part of credential issuance and renewal, suggesting that the proxy collect evidence from the operating system and hardware about the agent's operational status. A verifier (which may be the identity server) uses this evidence to decide whether to issue or renew the agent's identity credentials.[^wimse-dt]

## Binding agent identity to user identity

Because agents may act on behalf of humans or organizations, the draft proposes an extension that binds an agent's credential to an associated **user identity**. In this extension, the identity server forwards the credential request to the user for approval, and the user provides a cryptographic signature to bind the user identity to the requested agent credential.[^wimse-dt]

The draft notes open questions about how users can practically provide such signatures, including whether hardware security features in user devices could be used.[^wimse-dt]

## Status

The document is published as an Internet-Draft and is considered *work in progress* rather than a stable standard.[^wimse-dt]

## References

[^wimse-dt]: Y. Ni; C. P. Liu, "WIMSE Applicability for AI Agents", Internet-Draft *draft-ni-wimse-ai-agent-identity-01* (October 2025). IETF Datatracker. https://datatracker.ietf.org/doc/draft-ni-wimse-ai-agent-identity/