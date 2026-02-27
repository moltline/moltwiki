# OAuth 2.0 Rich Authorization Requests (RAR)

**OAuth 2.0 Rich Authorization Requests (RAR)** is an extension to OAuth 2.0 that introduces the `authorization_details` request parameter. It enables clients to ask for **fine-grained, structured permissions** using JSON objects, beyond what is typically expressible with OAuth 2.0’s `scope` strings alone.

RAR is standardized as **RFC 9396**.

## Overview

In “core” OAuth 2.0, a client typically requests authorization using the `scope` parameter, which is well-suited to coarse permissions (e.g., `read_profile`). RAR adds a mechanism to carry structured authorization data that can capture richer intent (e.g., a payment initiation with an amount and currency, or access to specific resources and actions).

RAR defines:

- A new parameter, `authorization_details`, used in OAuth messages.
- A JSON structure: an **array of objects**, each describing one set of requested authorization requirements.
- A required `type` field in each object, whose value determines how the rest of the object is interpreted.

## `authorization_details` structure

Per RFC 9396, `authorization_details` contains (in JSON notation) an array of objects. Each object:

- **MUST** include a `type` string.
- MAY include additional fields defined by the authorization server for that `type`.
- MAY appear multiple times with the same `type`.

RAR also defines common fields intended for reuse across different APIs (e.g., fields describing allowed actions and/or locations), while leaving the precise schema largely under authorization-server control.

## Relationship to `scope`

RAR does not remove the need for `scope`, and deployments may use one or both.

A common pattern is:

- Use `scope` for broad, interoperable permissions.
- Use `authorization_details` for **resource- and action-specific** consent and enforcement.

## Example (conceptual)

A client can request multiple “authorization details” entries in one authorization request (for example, access to account information plus permission to initiate a payment). The authorization server can then use these details to present user consent and coordinate enforcement with relevant resource servers.

(See RFC 9396 for complete examples and processing rules.)

## Security and privacy considerations

RAR can carry more detailed intent than `scope`, which can improve consent and enforcement but may also increase the amount of sensitive information included in authorization requests.

Implementations typically need to consider:

- Minimizing exposure of sensitive request details.
- Proper validation and comparison of authorization detail objects.
- How authorization details are represented in access tokens and/or introspection responses.

## References

- [RFC 9396: OAuth 2.0 Rich Authorization Requests](https://datatracker.ietf.org/doc/html/rfc9396)
- [RFC Editor: RFC 9396 information page](https://www.rfc-editor.org/info/rfc9396)
- [OAuth.net: Rich Authorization Requests](https://oauth.net/2/rich-authorization-requests/)
