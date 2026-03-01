# Web Bot Auth

**Web Bot Auth** is an Internet Engineering Task Force (IETF) work-in-progress architecture for identifying automated HTTP traffic using cryptographic signatures. It proposes that automated HTTP clients (“bots” and other agents) sign outbound requests using **HTTP Message Signatures** so that receiving servers (“origins”) can verify the sender’s identity with higher confidence than approaches such as User-Agent strings or IP allowlists.

## Overview

The architecture describes a model where an automated client (the *agent*) constructs an HTTP request and attaches a signature (as defined by HTTP Message Signatures). The receiving server validates the signature using the agent’s verification key, which can be discovered via mechanisms described by the Web Bot Auth drafts (e.g., a discovery header and/or published key material).

The motivation section highlights common shortcomings of existing bot-identification methods:

- **User-Agent strings** can be spoofed and are often overloaded for compatibility.
- **IP allowlists** can be difficult to manage and do not strongly bind identity to a service provider.
- **Shared secrets / API keys** do not scale well across the open web and complicate rotation.

By using request signing at the HTTP layer, Web Bot Auth aims to provide an interoperable mechanism that works through common proxy and gateway deployments.

## Relationship to agent ecosystems

Web Bot Auth is frequently discussed in the context of rising “agentic” traffic on the web, including AI assistants and automated clients that interact with websites and APIs. Its focus on verifiable request provenance has been referenced by some industry “agentic commerce” initiatives as a potential building block for distinguishing trusted automated clients from malicious automation.

## Status

Web Bot Auth is published as an **Internet-Draft** on the IETF Datatracker. Internet-Drafts are working documents that may change, be replaced, or expire; they are not standards-track RFCs.

## References

- T. Meunier, *HTTP Message Signatures for automated traffic Architecture* (Internet-Draft), IETF Datatracker, Oct 2025. https://datatracker.ietf.org/doc/draft-meunier-web-bot-auth-architecture/
