# SPIRE

**SPIRE** (the **SPIFFE Runtime Environment**) is an open source implementation of the [SPIFFE](SPIFFE.md) standards that provides a workload identity control plane for distributed systems. SPIRE can attest workloads and issue cryptographic identities (SPIFFE IDs and SVIDs) that applications can use for authentication and authorization, including mutual TLS (mTLS) and JWT-based mechanisms.[^spire-readme][^spiffe-site]

## Overview

SPIRE is typically deployed as:

- **SPIRE Server**: the control-plane component that maintains a registry of workload identities and issues credentials.
- **SPIRE Agent**: a node-level component that performs workload attestation and delivers credentials to workloads via the **SPIFFE Workload API**.[^spire-readme]

SPIRE’s goal is to replace static secrets (long-lived certificates, API keys) with **automated, short-lived, strongly attested workload identities** that can be used across heterogeneous environments (e.g., Kubernetes, VMs, multiple clouds).[^spiffe-site]

## SPIFFE IDs, SVIDs, and the Workload API

SPIRE issues identities and credentials defined by SPIFFE:

- **SPIFFE ID**: a URI-like identifier for a workload.
- **SVID (SPIFFE Verifiable Identity Document)**: the credential bound to a SPIFFE ID (commonly an X.509 SVID for mTLS, or a JWT SVID for token-based systems).
- **SPIFFE Workload API**: an API that workloads use to retrieve and rotate their SVIDs and trust bundles.[^spire-readme]

## Use cases

Common use cases described by the SPIFFE/SPIRE project include:[^spiffe-site]

- **Service-to-service authentication** using mTLS.
- **Zero trust** workload identity for microservices.
- **Authentication to infrastructure services** (e.g., secret stores, databases, cloud services) without embedding long-lived credentials.

## Project and governance

SPIRE is a project of the **Cloud Native Computing Foundation (CNCF)**.[^spire-readme]

## See also

- [SPIFFE](SPIFFE.md)
- [mTLS](mTLS.md)

## References

[^spiffe-site]: SPIFFE Project. “SPIFFE – Secure Production Identity Framework for Everyone” (website). https://spiffe.io/
[^spire-readme]: SPIFFE Project. *spiffe/spire* (GitHub repository README). https://github.com/spiffe/spire
