# OAuth 2.0 Resource Indicators (RFC 8707)

**OAuth 2.0 Resource Indicators** are an extension to the OAuth 2.0 authorization framework that lets a client explicitly tell an authorization server *which protected resource (resource server)* it wants an access token for, using the `resource` request parameter. The extension is standardized as **RFC 8707** (February 2020).

Resource Indicators are commonly discussed in the context of **token audience restriction** and mitigating **token mis-redemption** (a class of attacks where a token minted for one resource is presented to another).

## Overview

In OAuth, a client typically asks an authorization server for an access token, then presents that token to a protected resource (API). In deployments with multiple resources (or where a client may interact with many services), it can be useful for the authorization server to know the intended token recipient.

RFC 8707 defines a `resource` parameter that a client can include in:

- the **authorization request**, and/or
- the **access token request**

to indicate the target protected resource.

The parameter value:

- **MUST** be an absolute URI.
- **MUST NOT** include a fragment component.
- **SHOULD NOT** include a query component (though the RFC notes some cases where queries can be useful).

Multiple `resource` parameters may be used to request a token intended for multiple resources.

## Security considerations

RFC 8707 is motivated in part by security properties of bearer tokens. If an authorization server can reliably determine the intended recipient of a token, it can audience-restrict the token so that it is not usable at other resources.

The RFC also registers an OAuth error code:

- `invalid_target` — the requested resource is invalid, missing, unknown, or malformed.

## Relationship to Model Context Protocol (MCP)

The **Model Context Protocol (MCP)** authorization specification requires MCP clients to implement **Resource Indicators** as defined in RFC 8707.

One motivation described in MCP-related guidance is preventing **token mis-redemption**: a client uses a resource indicator when requesting a token so the authorization server can mint a token intended only for a specific MCP server (resource), reducing the risk that a token is used successfully at a different protected resource.

## See also

- [OAuth 2.0](https://datatracker.ietf.org/doc/html/rfc6749)
- [OAuth 2.1 (draft)](https://datatracker.ietf.org/doc/html/draft-ietf-oauth-v2-1)
- [Model Context Protocol (MCP)](Model%20Context%20Protocol%20(MCP).md)
- [Model Context Protocol (MCP) Authorization](Model%20Context%20Protocol%20(MCP)%20Authorization.md)

## References

- Campbell, B. *et al.* (2020). **Resource Indicators for OAuth 2.0 (RFC 8707)**. RFC Editor. https://www.rfc-editor.org/rfc/rfc8707
- Model Context Protocol. **Authorization** (draft). https://modelcontextprotocol.io/specification/draft/basic/authorization
- Auth0 (2025). **Model Context Protocol (MCP) Spec Updates from June 2025**. https://auth0.com/blog/mcp-specs-update-all-about-auth/
