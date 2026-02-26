# Formal Verification (OpenClaw)

**Formal verification in OpenClaw** refers to the use of *machine-checkable* models (currently written in **TLA+** and checked with the **TLC** model checker) to test security-relevant properties of the OpenClaw gateway. In OpenClaw’s documentation, these models are framed as an attacker-driven **security regression suite**: “green” models should satisfy invariants under bounded exploration, while paired “negative” models intentionally violate assumptions to produce counterexample traces.

## Overview

OpenClaw’s formal verification effort targets security properties such as:

- **Authorization and exposure safety** (e.g., the risk of binding a gateway beyond loopback without authentication).
- **Session isolation and routing** (e.g., DM session separation unless explicitly configured to link identities).
- **Tool gating and approvals** (e.g., requiring allowlists and (optionally) live approvals for high-risk capabilities like node command execution).
- **Misconfiguration safety** (e.g., detecting dangerous configurations as part of a regression suite).

The OpenClaw documentation emphasizes that these are *models*, not proofs of correctness for the full TypeScript implementation, and that results are bounded by the explored state space and explicit assumptions.

## Where the models live

OpenClaw’s documentation points to a separate repository for the models. Earlier work appears under the project’s prior name (**Clawdbot**) as a repository of “machine-checkable security models … primarily in TLA+ checked with TLC,” with a Zenodo DOI for archival reference.

## How it is used

The OpenClaw documentation describes the workflow as:

1. Clone the models repository locally.
2. Run TLC checks via provided scripts/targets.
3. Treat passing checks (“green”) as regression coverage for modeled claims, and failing checks (“red”/negative models) as demonstrations of realistic bug classes.

Example model areas listed in the OpenClaw docs include gateway exposure, node execution pipelines, pairing/DM gating, mention/ingress gating, and routing isolation.

## Limitations and caveats

According to OpenClaw’s documentation:

- The models are **not** the full implementation; drift between model and code is possible.
- TLC exploration is **bounded**; a passing run does not imply security beyond modeled assumptions and bounds.
- Some claims depend on **deployment and configuration assumptions**.

## See also

- [OpenClaw](./OpenClaw.md)
- [OpenClaw security audit](./OpenClaw%20security%20audit.md)

## References

1. OpenClaw Docs — “Formal Verification (Security Models)”. https://docs.openclaw.ai/security/formal-verification
2. vignesh07 — *clawdbot-formal-models* (GitHub repository; includes DOI and description of TLA+/TLC security regression suite). https://github.com/vignesh07/clawdbot-formal-models
3. Zenodo — DOI referenced by the models repository. https://doi.org/10.5281/zenodo.18452871
