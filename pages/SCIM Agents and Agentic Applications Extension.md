# SCIM Agents and Agentic Applications Extension

The **SCIM Agents and Agentic Applications Extension** is an Internet-Draft that proposes extending the **System for Cross-domain Identity Management (SCIM)** protocol to represent and provision **AI agents** and **agentic applications** across organizational boundaries.

The draft introduces new SCIM 2.0 resource types and schemas intended to let identity providers and service providers manage non-human identities (e.g., autonomous agents, bots, assistants) using existing SCIM infrastructure and lifecycle workflows.

## Background

SCIM is an IETF standards-track protocol and schema suite for exchanging identity information—primarily users and groups—between identity providers and service providers. The extension draft argues that as agentic software becomes more common, organizations will need similar cross-domain lifecycle management for agents and agent-hosting applications, and that reusing SCIM can reduce fragmentation relative to creating entirely new identity protocols.

## Draft overview

The Internet-Draft titled *“SCIM Agents and Agentic Applications Extension”* (draft identifier **draft-scim-agent-extension-00**) describes:

- **Core schema extensions**, including changes to SCIM configuration and core objects.
- New SCIM **ResourceTypes** and schemas for:
  - **Agent**
  - **Agentic application**

The draft also includes JSON schema representations and discusses security considerations.

## Proposed resource types

### Agent

The draft defines an **Agent** resource type intended to represent an agent as a first-class SCIM-managed identity. As described in secondary commentary, the schema is intended to support common identity-management needs such as naming, activation state, ownership/responsibility metadata, and linkage to the applications that host the agent.

### Agentic application

The draft defines an **AgenticApplication** (agentic application) resource type intended to represent an application that hosts or exposes agents. This can be used to model agent-hosting systems and their relationships to the agents they contain.

## Relationship to the agent ecosystem

The draft explicitly situates itself within a broader ecosystem of agent interoperability efforts, and lists several agent-related protocols/directories as examples of emerging standards activity.

## Draft status and availability

The draft is published on the IETF Datatracker as **draft-scim-agent-extension-00** (Oct 2025, expires Apr 2026) and is also available as an IETF HTML archive.

The Datatracker page also links to the draft’s source repository and issue tracker.

## Protocol and schema details (selected)

### ServiceProviderConfig discovery

The draft specifies that SCIM servers supporting the extension **MUST** advertise support via the SCIM **/ServiceProviderConfig** endpoint using an `agentExtension` object with booleans indicating support for the extension and for the `Agent` and `AgenticApplication` resource types.

### Agent resource type and filtering

The draft defines an `Agent` resource type with endpoint **`/Agents`** and schema URI **`urn:ietf:params:scim:schemas:core:2.0:Agent`**.

It also **recommends** that service providers implement equality filtering on `name` and `externalId` so clients can locate agents when they do not know the SCIM `id`.

### Agent core schema (selected attributes)

In the HTML archive, the `Agent` core schema defines `name` as **REQUIRED**, and includes optional attributes such as `displayName`, `active`, `description`, and `agentType` (among others).

## References

- M. Abbey; R. S. Cohen. *SCIM Agents and Agentic Applications Extension (draft-scim-agent-extension-00).* IETF Internet-Draft, Oct 2025. https://datatracker.ietf.org/doc/draft-scim-agent-extension/00/ (work in progress)
- M. Abbey; R. S. Cohen. *SCIM Agents and Agentic Applications Extension.* IETF Internet-Draft (HTML). https://www.ietf.org/archive/id/draft-abbey-scim-agent-extension-00.html (work in progress)
- IETF Datatracker. *SCIM Agents and Agentic Applications Extension — meeting slides (IETF 124, SCIM WG).* https://datatracker.ietf.org/doc/slides-124-scim-scim-agents-and-agentic-applications-extension/
- WorkOS. *SCIM for AI: Inside the new IETF draft for agent and agentic application provisioning.* https://workos.com/blog/scim-agents-agentic-applications
