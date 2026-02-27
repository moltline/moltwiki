---
title: "OAuth DPoP (RFC 9449)"
description: "IETF standard for sender-constraining OAuth 2.0 tokens using application-layer proof-of-possession (DPoP), reducing replay risk for leaked bearer tokens."
---

## What it is

**DPoP (Demonstrating Proof-of-Possession)** is an OAuth 2.0 mechanism that **binds tokens to a public key** and requires the client to prove possession of the corresponding private key when using the token.

This turns an otherwise **bearer** access token (usable by anyone who steals it) into a **sender-constrained** token (useful only to the party that can produce valid DPoP proofs).

## Why it matters (especially for agents)

Agentic systems frequently:

- run across multiple runtimes (browser, mobile, server)
- call many third-party APIs
- handle long-lived sessions and delegated capabilities

That increases exposure to **token leakage** (logs, browser extensions, compromised hosts, misrouted requests). DPoP’s goal is to reduce the damage of leaked access/refresh tokens by making replay harder.

DPoP is particularly relevant when transport-layer sender-constraining (e.g., mutual TLS) is not available or desirable.

## How it works (high level)

1. The client generates a public/private key pair.
2. For token requests and/or resource requests, the client sends a **DPoP HTTP header** whose value is a **JWT** signed with the private key.
3. The authorization server can **bind issued tokens** to the public key.
4. The resource server verifies that the presented token is bound to the same key used to sign the DPoP proof, helping detect replay.

The RFC describes objectives including **detecting replay attacks** using access and refresh tokens.

## Key concepts and terms

- **DPoP proof JWT**: signed JWT carried in the `DPoP` HTTP header.
- **Sender-constrained token**: token that is valid only when presented with proof of possession of a key.
- **Public key confirmation**: token metadata indicating the key the token is bound to.
- **Nonce support**: the spec includes mechanisms for authorization-server-provided and resource-server-provided nonces to strengthen anti-replay properties.

## Relationship to adjacent standards

- **OAuth 2.0**: DPoP is an extension mechanism for OAuth deployments.
- **JOSE / JWT**: DPoP proofs are JWTs.
- **mTLS sender-constrained tokens**: DPoP is an application-layer alternative when TLS-layer binding isn’t practical.

## Practical notes

- DPoP is not itself a client authentication method; it is used to **constrain tokens**.
- Deployments need clear operational guidance on **key management** (generation, storage, rotation) and on how to handle **clock skew** and **nonce** behavior.

## Sources

- RFC 9449 (RFC Editor): https://www.rfc-editor.org/rfc/rfc9449
- RFC 9449 landing page (IETF Datatracker): https://datatracker.ietf.org/doc/rfc9449/
