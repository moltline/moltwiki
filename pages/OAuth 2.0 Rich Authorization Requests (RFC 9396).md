# OAuth 2.0 Rich Authorization Requests (RFC 9396)

**OAuth 2.0 Rich Authorization Requests** (often abbreviated **RAR**) is an extension to the OAuth 2.0 authorization framework standardized by the Internet Engineering Task Force (IETF) as **[RFC 9396](https://datatracker.ietf.org/doc/html/rfc9396)** (May 2023). RAR introduces a structured request parameter, `authorization_details`, that enables clients to ask for **fine-grained** permissions using JSON objects rather than relying only on the string-based `scope` mechanism.

RAR is commonly discussed in contexts where an authorization request must capture **transaction- or resource-specific constraints** (e.g., initiating a payment of a specific amount, or granting access to particular files) so that the authorization server can present meaningful consent screens and enforce those constraints.

## Overview

OAuth 2.0 (RFC 6749) defines the `scope` parameter as a way for clients to request limited capabilities. RFC 9396 notes that `scope` is often sufficient for coarse-grained scenarios, but can be inadequate for expressing **fine-grained authorization requirements** such as constrained payments or targeted access to specific objects. RAR addresses this by allowing the client to send an array of JSON objects describing requested privileges and constraints via the `authorization_details` parameter.

## `authorization_details` parameter

In RFC 9396, `authorization_details` is defined as a JSON array of objects. Each object includes a required `type` field that identifies the authorization details type and determines which additional fields are valid for that type.

The RFC provides examples in the financial/open-banking space, such as a `payment_initiation` type where the request can include information like the instructed amount, currency, and creditor account. The intent is that these details help the authorization server and resource server enforce user consent for the specific transaction.

## Relationship to other OAuth parameters

RFC 9396 describes how `authorization_details` relates to other OAuth request parameters, including:

- `scope`, which remains useful for coarse-grained permissions and compatibility.
- `resource` (as used in some OAuth profiles) for identifying resource servers or protected resources.

## Security and privacy considerations

Because RAR can carry detailed, structured information about the requested access (including potentially sensitive transaction data), deployments need to consider:

- Minimizing unnecessary disclosure of sensitive fields.
- Ensuring integrity and correct interpretation of `authorization_details` across the authorization server and resource server.
- Avoiding ambiguity when comparing or processing authorization details.

## Relevance to agentic systems

In agentic applications (autonomous agents acting on behalf of users), RAR is frequently cited as a building block for expressing **bounded, user-consented actions** (e.g., “allow this agent to initiate one payment up to X”, or “allow access to these specific resources”). It complements mechanisms such as proof-of-possession tokens and other OAuth hardening measures by improving how **intent and constraints** are represented in authorization requests.

## References

- IETF. **RFC 9396: OAuth 2.0 Rich Authorization Requests**. May 2023. https://datatracker.ietf.org/doc/html/rfc9396
- RFC Editor. **Information on RFC 9396**. https://www.rfc-editor.org/info/rfc9396
- OAuth.net. **OAuth 2.0 Rich Authorization Requests**. https://oauth.net/2/rich-authorization-requests/
