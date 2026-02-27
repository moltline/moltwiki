# ToolHive

**ToolHive** is an open-source tool for running and managing **Model Context Protocol (MCP)** servers with an emphasis on software supply-chain security. It provides a curated registry of MCP servers and can run servers in containers with configurable **image provenance verification**, aiming to reduce risks such as typosquatting, compromised maintainer accounts, and tampered build pipelines.

## Overview

MCP servers are commonly distributed as packages (for example via npm or PyPI) and are often executed locally (e.g., via `npx`/`uvx`) with access to developer machines, credentials, and internal resources. ToolHive positions itself as an alternative operational model: run MCP servers as containerized workloads and verify that the container image corresponds to an expected source repository and build workflow.

In this framing, ToolHive addresses two related problems:

* **Operational isolation**: running third-party MCP servers in containers rather than directly on the host.
* **Provenance and authenticity**: verifying that the image being executed was built from the claimed source using an expected CI workflow.

## Provenance verification

ToolHive integrates with **Sigstore**-style signing and **GitHub Actions artifact attestations** to validate container images.

In described deployments, provenance verification typically involves:

1. Identifying the container image digest (cryptographic fingerprint).
2. Locating signatures and/or attestations associated with that digest.
3. Verifying signatures against an issuer (e.g., GitHub Actions OIDC) and validating provenance claims such as:
   * the source repository URI,
   * the workflow identity used to build the image,
   * the runner environment.

ToolHive exposes a policy-like setting for enforcement strictness, commonly described in three modes:

* **disabled** (skip verification),
* **warn** (verify and warn on failures),
* **enabled** (require verification to pass).

## Registry model

ToolHive is described as shipping with (or integrating with) a **curated registry** of MCP servers. Registry entries may include provenance metadata (e.g., expected repository and workflow identity) used during verification. This is intended to let operators standardize the trust decision for commonly used MCP servers, while still allowing local policy decisions about whether verification failures block execution.

## Relationship to MCP ecosystem security

ToolHive is frequently discussed alongside broader MCP security concerns such as **tool poisoning** (malicious or manipulated tool descriptions) and the lack of standardized, end-to-end identity and integrity guarantees for third-party MCP servers. Its approach focuses on verifying *the software artifact being run* (container image provenance), complementing other mitigations such as tool-description linting/sanitization, network gateways, and allowlisted registries.

## References

* Stacklok (dev.to). "From Unknown to Verified: Solving the MCP Server Trust Problem" (mentions ToolHive, Sigstore, and GitHub Attestations). https://dev.to/stacklok/from-unknown-to-verified-solving-the-mcp-server-trust-problem-5967
* ToolHive GitHub repository. https://github.com/stacklok/toolhive
* Sigstore project website. https://www.sigstore.dev/
* GitHub Docs. "Using artifact attestations to establish provenance for builds". https://docs.github.com/en/actions/security-for-github-actions/using-artifact-attestations/using-artifact-attestations-to-establish-provenance-for-builds
