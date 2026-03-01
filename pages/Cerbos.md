# Cerbos

Cerbos is an open-source authorization layer (policy decision point) for adding fine-grained access control to applications and APIs. Cerbos evaluates authorization decisions using policies (for example, role- and attribute-based rules) and returns allow/deny outcomes to the calling service.

In the context of AI agents and the [Model Context Protocol (MCP)](Model%20Context%20Protocol%20%28MCP%29.md), Cerbos has been presented as a way to externalize “who can do what” decisions for MCP tool calls, so that MCP servers can consult an authorization service before executing sensitive operations.

## Overview

Authorization systems commonly separate:

- **Policy enforcement** (the application or gateway that intercepts a request), from
- **Policy decision** (a dedicated component that evaluates policies and returns an allow/deny result).

Cerbos is designed to act as a policy decision point that applications can query at runtime. This approach is often used to avoid hard-coding authorization logic into each service and to support evolving policies without redeploying application code.

## Cerbos and MCP tool authorization

MCP enables clients (including agentic clients) to call tools exposed by MCP servers. MCP’s HTTP transport can use OAuth-based authorization to authenticate and authorize requests at the transport level.

However, OAuth scopes and token validation typically do not, by themselves, express fine-grained business rules (for example, “a manager can approve expenses up to $1,000” or “a user can read only their own records”). Cerbos’ documentation and blog materials describe integrating an MCP server with Cerbos so that each tool invocation is checked against policy before being executed.

## Related concepts

- **Policy-based access control (PBAC)**: a general term for declarative authorization rules evaluated at runtime.
- **ABAC / RBAC**: attribute-based and role-based access control models, often combined in practice.
- **Confused deputy problem**: a class of security issue relevant when an agent or intermediary performs actions using privileges broader than intended.

## See also

- [Model Context Protocol (MCP) Authorization](Model%20Context%20Protocol%20%28MCP%29%20Authorization.md)
- [Enterprise-Grade Security for the Model Context Protocol (MCP).](Enterprise-Grade%20Security%20for%20the%20Model%20Context%20Protocol%20%28MCP%29.md)
- [AI Agent Gateway (MCP + OPA + Ephemeral Runners).](AI%20Agent%20Gateway%20%28MCP%20%2B%20OPA%20%2B%20Ephemeral%20Runners%29.md)

## References

- Cerbos. “MCP authorization: Securing Model Context Protocol servers with fine-grained access control.” https://www.cerbos.dev/blog/mcp-authorization
- Cerbos. Documentation. https://docs.cerbos.dev/
- Model Context Protocol. “Authorization.” https://modelcontextprotocol.io/specification/2025-03-26/basic/authorization
