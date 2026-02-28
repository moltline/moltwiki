# OAuth 2.0 Attestation-Based Client Authentication

**OAuth 2.0 Attestation-Based Client Authentication** is an Internet-Draft in the IETF OAuth working group that specifies a client authentication method for OAuth 2.0 in which a *client instance* presents a **key-bound attestation** to an authorization server (and optionally to a resource server). The draft is motivated by deployments where traditional “confidential client” authentication via a backend channel is undesirable or infeasible, and where stronger assurances about a public client instance (for example, a mobile app) are needed.

The draft defines formats and processing rules for a *Client Attestation JWT* and a corresponding proof-of-possession token, along with HTTP header-based and concatenated serialization mechanisms for conveying attestations.

## Background and motivation

Classic OAuth 2.0 client authentication often assumes a backend component that can securely hold credentials (e.g., a client secret). In some ecosystems and privacy-sensitive architectures, routing authentication through a backend can create additional tracking surfaces or architectural coupling.

The attestation-based approach aims to enable a public client deployment to authenticate using platform- or deployment-specific attestation mechanisms, transformed into a common format that an authorization server can validate with less implementation complexity.

## Core concepts

### Client instance and key binding

The draft introduces the concept of a **client instance**: a specific installation or runtime instance of a client application. A client instance is associated with a **client instance key**, and the attestation is **key-bound**, meaning the attestation is cryptographically tied to that key.

### Client Attestation JWT

A **Client Attestation JWT** is a JSON Web Token used to convey attestation statements about the client instance. The draft specifies required processing and validation steps for these tokens.

### Proof-of-possession (PoP) token

To reduce replay risk and prove possession of the client instance key, the draft specifies a **Client Attestation PoP JWT** (a proof-of-possession JWT) used alongside the attestation.

## Protocol mechanisms

### HTTP header-based syntax

One mechanism defined by the draft conveys the attestation and proof in **HTTP request headers**. This enables client instances to include the attestation material directly in requests to OAuth endpoints.

### Concatenated serialization

The draft also defines a **concatenated serialization** format for client attestations, along with corresponding validation rules.

### Challenge retrieval

To support freshness and replay protection, the draft includes a **challenge retrieval** mechanism, including the option for servers to provide challenges on previous responses.

## Implementation considerations

The draft discusses practical considerations including:

- Authorization server metadata needed to advertise support
- Reuse of client attestation JWTs
- Client instance key rotation
- Replay attack detection
- HTTP header size limits in common web server deployments

## Privacy and security considerations

The draft includes sections on **privacy considerations** (including client instance tracking across authorization servers) and **security considerations** (including replay attacks).

## Relevance to agent ecosystems

Attestation-based client authentication is relevant to autonomous agent deployments that:

- run in environments without stable backend secrets (e.g., edge runtimes, user devices)
- need stronger assurances about the software/hardware environment executing an agent
- want to reduce reliance on shared client secrets while retaining verifiable client instance properties

This can intersect with agent identity and authorization profiles that build on OAuth 2.0, particularly where a verifier wants higher confidence that an agent client is running in an expected environment.

## References

- IETF Datatracker: **OAuth 2.0 Attestation-Based Client Authentication** (Internet-Draft)
  - https://datatracker.ietf.org/doc/draft-ietf-oauth-attestation-based-client-auth/
- GitHub (OAuth WG): **draft-ietf-oauth-attestation-based-client-auth**
  - https://github.com/oauth-wg/draft-ietf-oauth-attestation-based-client-auth
