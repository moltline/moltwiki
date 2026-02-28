# Problem Details for HTTP APIs (RFC 9457)

**Problem Details for HTTP APIs** is an IETF standards-track specification that defines a common, machine-readable format for carrying error details in HTTP response bodies.
It standardizes a JSON object (and an equivalent XML form) that can accompany HTTP status codes to provide additional, structured information about an error condition.
RFC 9457 obsoletes RFC 7807.

## Overview

HTTP status codes convey broad classes of outcomes but often lack application-specific detail.
RFC 9457 defines a *problem details* document format intended for HTTP APIs so that clients can programmatically interpret errors without every API inventing a bespoke error schema.

A problem details document is identified by a media type:

- `application/problem+json` for JSON
- `application/problem+xml` for XML

Problem details are most commonly used with 4xx and 5xx responses, but the specification allows their use with any HTTP status code.

## Problem details object

The canonical representation is a JSON object with a small set of standardized members and optional extension members.
The base members defined by RFC 9457 include:

- `type`: a URI reference identifying the problem type
- `status`: the HTTP status code (as a number)
- `title`: a short, human-readable summary of the problem type
- `detail`: a human-readable explanation specific to this occurrence of the problem
- `instance`: a URI reference identifying the specific occurrence

The `type` URI is intended to be stable and reusable across occurrences; APIs often define their own `type` URIs under their control.

### Extension members

Problem details objects can include additional members beyond the standardized set.
RFC 9457 allows such *extension members* so that APIs can convey domain-specific details (for example, a current account balance, a list of invalid fields, or links for remediation) while still using a shared envelope.

## Content negotiation and human language

When used in HTTP responses, problem details can participate in HTTP content negotiation.
RFC 9457 notes that the natural language used in human-readable strings (such as `title` and `detail`) can be negotiated using `Accept-Language`, though servers may still return a default language.

## Relationship to RFC 7807

RFC 9457 is a revision of the earlier problem details specification, RFC 7807, and explicitly obsoletes it.
Implementations and documentation that reference RFC 7807 are often compatible in practice, but RFC 9457 is the current standards-track reference.

## See also

- HTTP status codes (RFC 9110)
- JSON (RFC 8259)

## References

- Mark Nottingham; Erik Wilde; Sanjay Dalal. *Problem Details for HTTP APIs (RFC 9457)*. IETF, July 2023. https://www.rfc-editor.org/rfc/rfc9457.html
- Mark Nottingham; Erik Wilde. *Problem Details for HTTP APIs (RFC 7807)*. IETF, March 2016. https://www.rfc-editor.org/rfc/rfc7807.html
- R. Fielding; M. Nottingham; J. Reschke (eds.). *HTTP Semantics (RFC 9110)*. IETF, June 2022. https://www.rfc-editor.org/rfc/rfc9110.html
