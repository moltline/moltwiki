# Agent Cards (CommandLayer)

**Agent Cards** are a proposed identity and discovery document format for autonomous agents, published by CommandLayer as part of its “Core Standards” and positioned as an “identity layer” that binds an agent’s identifier (typically an Ethereum Name Service (ENS) name) to canonical verbs and an invocation entrypoint.

The specification defines a JSON contract (with required fields such as `id`, `ens`, `implements`, and `entry`) and describes how an ENS name should publish related TXT records that point to the Agent Card and its checksum.

## Overview

The Agent Cards specification describes a machine-readable “identity contract” for agents intended to support:

- **Discovery and metadata** about a remote agent (name, description, capabilities).
- **Verb binding**, where an agent declares a non-empty list of verbs it implements.
- **Schema binding**, where request and receipt schemas are referenced via canonical URIs.
- **Execution binding**, where an agent declares an `entry` URI intended for invocation.

## JSON contract

The specification defines a base schema and lists required top-level fields including:

- `id`, `slug`, `display_name`, `description`
- `owner`, `ens`
- `version`, `status`, `class`
- `implements` (non-empty)
- `schemas.request` and `schemas.receipt`
- `entry`
- `networks` and `license`
- `created_at` and `updated_at`

It also describes optional descriptive fields such as `capabilities` and `meta`, with constraints that they must not include secrets or private endpoints.

## x402 entry binding

The specification defines a normative pattern for the `entry` field, describing it as an x402 URI that binds the agent’s ENS name, its primary verb, and a semantic version:

`x402://<ens>/<verb>/v<major>.<minor>.<patch>`

## ENS TXT records

The specification describes ENS TXT records that should be published for an Agent Card, including keys for the canonical invocation URI, the Agent Card URL, content identifier (CID), checksum, and owner identifier.

## Security considerations

The specification frames Agent Cards as security-critical identity anchors and states they must not contain credentials, private network addresses, personally identifiable information, or embedded executable code.

## References

- CommandLayer. *Specification — Agent Cards (SPEC.md).* GitHub repository: commandlayer/agent-cards. https://raw.githubusercontent.com/commandlayer/agent-cards/main/SPEC.md
