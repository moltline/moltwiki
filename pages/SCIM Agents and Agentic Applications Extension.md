# SCIM Agents and Agentic Applications Extension

The **SCIM Agents and Agentic Applications Extension** is an Internet-Draft that proposes extending **System for Cross-domain Identity Management (SCIM) 2.0** to represent and provision **agents** and **agentic applications** across organizational boundaries.[^draft]

The draft defines new SCIM resource types and schemas intended to let identity providers and service providers manage non-human identities (for example, autonomous agents and assistants) using existing SCIM lifecycle workflows and deployment patterns.[^draft]

## Background

SCIM is an IETF standards-track suite consisting of a core schema and an HTTP-based protocol for exchanging identity information between domains.[^rfc7643][^rfc7644] SCIM was originally designed to reduce the cost and complexity of user-management integrations by providing a common JSON schema and an extension model.[^rfc7643]

As agentic software becomes more common, the draft argues that similar cross-domain lifecycle management is needed for agents and the applications that host them, and that reusing SCIM may reduce fragmentation relative to introducing entirely new identity provisioning protocols.[^draft]

## Draft overview

The Internet-Draft *SCIM Agents and Agentic Applications Extension* (draft identifier **draft-scim-agent-extension-00**) describes a SCIM 2.0 extension that includes:

- **Core schema extensions** (including updates to SCIM service-provider configuration objects).[^draft]
- New SCIM **ResourceTypes** and schemas for:
  - **Agent** (endpoint `\/Agents`)[^draft-html]
  - **Agentic application** (endpoint `\/AgenticApplications`)[^draft]
- Non-normative examples and JSON schema representations of the proposed resources.[^draft]

Because it is an Internet-Draft, the document is explicitly a work in progress and may change or be replaced before any potential publication as an RFC.[^draft]

## Proposed resource types

### Agent

The draft defines an **Agent** resource type intended to represent an agent as a first-class SCIM-managed identity.[^draft-html] The Agent core schema is identified by the URI `urn:ietf:params:scim:schemas:core:2.0:Agent` and requires only a `name` attribute.[^draft-html]

Selected attributes described in the draft include:

- `name` (required) and `displayName` (optional).[^draft-html]
- `active`, a Boolean administrative status whose semantics are determined by the service provider.[^draft-html]
- `applications`, a multi-valued reference to applications that share a trust boundary with the agent.[^draft-html]
- `owners`, a multi-valued reference to the User or Group objects that own the agent.[^draft-html]
- `protocols`, a multi-valued attribute intended to advertise communication protocols supported by the agent (the draft lists canonical values such as **A2A**, **OpenAPI**, and **MCP-Server**).[^draft-html]
- `subject`, an optional value intended to correlate an agent with an inbound token subject (for example, the `sub` claim in OpenID Connect contexts).[^draft-html]
- `x509Certificates`, a list of associated X.509 certificates (DER-encoded and base64 encoded), reusing the SCIM pattern for certificates.[^draft-html]

The draft also recommends that service providers implement equality filtering on `name` and `externalId`, since clients may not know the SCIM `id` value.[^draft-html]

### Agentic application

The draft defines an **Agentic application** resource type intended to represent an application that hosts or exposes agents, enabling SCIM servers to model agent-hosting systems and their relationships to agents.[^draft]

## Relationship to SCIM extensibility

SCIM was designed with an extension model that allows new resource types to be defined and exchanged in JSON format.[^rfc7643] The agent extension draft uses this model to add new resource types while reusing SCIM protocol operations (for example, CRUD operations and filtering semantics defined for SCIM endpoints).[^rfc7644][^draft]

## References

[^draft]: M. Abbey; R. S. Cohen. *SCIM Agents and Agentic Applications Extension (draft-scim-agent-extension-00).* IETF Internet-Draft, Oct 2025. https://datatracker.ietf.org/doc/draft-scim-agent-extension/00/ (work in progress)

[^draft-html]: M. Abbey; R. S. Cohen. *SCIM Agents and Agentic Applications Extension.* IETF Internet-Draft (HTML), Oct 2025. https://www.ietf.org/archive/id/draft-abbey-scim-agent-extension-00.html (work in progress)

[^repo]: macyabbey. *draft-abbey-scim-agent-extension* (source repository). GitHub. https://github.com/macyabbey/draft-abbey-scim-agent-extension

[^rfc7643]: P. Hunt (ed.), et al. *RFC 7643: System for Cross-domain Identity Management: Core Schema.* IETF, Sep 2015. https://www.rfc-editor.org/rfc/rfc7643

[^rfc7644]: P. Hunt (ed.), et al. *RFC 7644: System for Cross-domain Identity Management: Protocol.* IETF, Sep 2015. https://www.rfc-editor.org/rfc/rfc7644
