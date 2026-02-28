# OAuth 2.0 Protected Resource Metadata (RFC 9728)

## Summary

**OAuth 2.0 Protected Resource Metadata** is an IETF Standards Track specification that defines a JSON metadata document a client (or an authorization server) can fetch to learn how to interact with an OAuth 2.0 **protected resource** (i.e., a resource server / API). It is intended to parallel patterns used for **authorization server metadata** ([RFC 8414](https://www.rfc-editor.org/rfc/rfc8414)) and **dynamic client registration** ([RFC 7591](https://www.rfc-editor.org/rfc/rfc7591)).

The metadata is published at a deterministic **`.well-known`** location derived from the protected resource’s **resource identifier** (a HTTPS URL without a fragment), and can be provided either as an unsigned JSON document or as **signed claims in a JWT**.

## Why it matters

In OAuth deployments, clients often need to know details about a resource server beyond “here is an access token”:

- which **authorization server(s)** can be used to obtain tokens for that resource
- which **scopes** make sense for that resource
- how to present bearer tokens (e.g., `Authorization` header)
- where to find the resource server’s **JWK Set** (for verifying signed responses, etc.)

RFC 9728 standardizes a way to publish and discover this information, reducing ad-hoc configuration and enabling more interoperable discovery flows.

## Core concepts

### Protected resource and resource identifier

RFC 9728 uses **resource identifier** in the sense of OAuth 2.0 resource indicators: a URL identifying the protected resource, using `https` and **no fragment** component. The spec notes that resource identifiers **SHOULD NOT** include a query component (per [RFC 8707](https://www.rfc-editor.org/rfc/rfc8707)), but recognizes that some deployments may need it.

### Deterministic well-known metadata location

A protected resource that supports RFC 9728 publishes its metadata at a **well-known URI** derived from the resource identifier (using the `.well-known` mechanism from [RFC 8615](https://www.rfc-editor.org/rfc/rfc8615)).

This deterministic binding is a security feature: it helps prevent an attacker from publishing “metadata about” a resource identifier that is not actually authoritative for that resource (see RFC 9728 security considerations).

### Unsigned vs signed metadata

RFC 9728 allows two representations:

- **Unsigned JSON metadata** (self-asserted by the protected resource)
- **Signed protected resource metadata** as claims in a **JWT**, where the issuer vouches for the metadata (analogous to a software statement in dynamic client registration)

## Metadata fields (selected)

RFC 9728 registers a set of metadata parameters for protected resources. Commonly relevant ones include:

- `resource` (REQUIRED): the protected resource’s resource identifier.
- `authorization_servers` (OPTIONAL): a JSON array of authorization server **issuer identifiers** (as defined by RFC 8414) that can be used with this protected resource.
- `scopes_supported` (RECOMMENDED): scopes used to request access to this protected resource.
- `bearer_methods_supported` (OPTIONAL): supported ways to present bearer tokens, with defined values corresponding to [RFC 6750](https://www.rfc-editor.org/rfc/rfc6750) (e.g., `header`, `body`, `query`).
- `jwks_uri` (OPTIONAL): URL of the protected resource’s JWK Set, used for publishing public keys (e.g., to verify signed resource responses).

The spec also defines human-readable fields such as `resource_name` and documentation/policy/TOS URLs.

## Interaction with other OAuth specs

RFC 9728 is designed to work with, and be referenced by, other OAuth profiles and extensions. For example:

- **Authorization server discovery** uses issuer-based metadata via RFC 8414.
- **Bearer token usage** aligns with RFC 6750.
- **Resource indicators** (RFC 8707) influence the definition of the resource identifier.
- Profiles that use **signed HTTP responses** or message signing can use `jwks_uri` to publish verification keys.

## References

- M. Jones, P. Hunt, A. Parecki. **OAuth 2.0 Protected Resource Metadata**. RFC 9728, April 2025. 
  - RFC Editor: https://www.rfc-editor.org/rfc/rfc9728 
  - Datatracker: https://datatracker.ietf.org/doc/rfc9728/ 
  - Info page: https://www.rfc-editor.org/info/rfc9728
- B. Campbell, et al. **OAuth 2.0 Authorization Server Metadata**. RFC 8414. https://www.rfc-editor.org/rfc/rfc8414
- J. Bradley, et al. **OAuth 2.0 Dynamic Client Registration Protocol**. RFC 7591. https://www.rfc-editor.org/rfc/rfc7591
- M. Jones, et al. **OAuth 2.0 Bearer Token Usage**. RFC 6750. https://www.rfc-editor.org/rfc/rfc6750
- J. Richer. **Resource Indicators for OAuth 2.0**. RFC 8707. https://www.rfc-editor.org/rfc/rfc8707
- M. Nottingham, E. Wilde. **Well-Known Uniform Resource Identifiers (URIs)**. RFC 8615. https://www.rfc-editor.org/rfc/rfc8615
