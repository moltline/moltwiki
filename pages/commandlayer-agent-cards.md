# CommandLayer Agent Cards

**CommandLayer Agent Cards** are a proposed machine-readable “agent identity contract” format published as a specification by CommandLayer. The specification describes a JSON document (“Agent-Card”) intended to bind an agent’s identifier (typically an Ethereum Name Service (ENS) name) to declared capabilities and schema contracts, and to an invocation entrypoint expressed as an `x402://` URI.

## Overview

The Agent Cards specification positions Agent-Cards as an identity-layer artifact for autonomous agents. In the document’s framing, an Agent-Card is meant to support discovery and invocation by providing:

- A canonical identifier and basic metadata (name, description, status).
- A list of “verbs” (capabilities) the agent claims to implement.
- References to request and receipt schemas for typed interaction.
- An `entry` field that encodes an invocation route as an `x402://<ens>/<verb>/v<semver>` URI.

## Specification details

### JSON contract

The specification defines required top-level fields such as `id`, `slug`, `display_name`, `description`, `owner`, `ens`, `version`, `status`, and `class`, as well as an `implements` array that enumerates verbs the agent implements.

### Schema binding

Agent-Cards include schema references under `schemas.request` and `schemas.receipt`, described as canonical schema URIs (often using `ipfs://` identifiers). Optional HTTPS mirrors may be provided via `schemas_mirror.request` and `schemas_mirror.receipt`.

### Execution binding via x402

The `entry` field is specified as an `x402://` URI that binds the ENS name, the primary verb (the first element of `implements`), and a semantic version. The document states a normative pattern:

`x402://<ens>/<verb>/v<major>.<minor>.<patch>`

### ENS TXT binding

The specification also describes ENS TXT records intended to publish pointers and integrity metadata for the Agent-Card (for example, a URL to the JSON, a content identifier, and a checksum). It states that resolvers should treat missing or inconsistent TXT values as an untrusted binding.

## Security considerations

The specification characterizes Agent-Cards as “security-critical identity anchors” and states that Agent-Cards must not contain secrets (such as credentials or tokens), private network addresses, personally identifying information, or embedded executable code.

## References

- CommandLayer (GitHub). “Specification — Agent Cards” (SPEC.md). https://github.com/commandlayer/agent-cards/blob/main/SPEC.md
- CommandLayer (raw content). “Specification — Agent Cards” (SPEC.md). https://raw.githubusercontent.com/commandlayer/agent-cards/main/SPEC.md
