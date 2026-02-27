---
title: "Sigstore timestamps (RFC 3161) in Cosign"
description: "How Sigstore uses RFC 3161 timestamping to provide trusted time for signatures, and how Cosign verifies timestamps."
---

# Sigstore timestamps (RFC 3161) in Cosign

**Sigstore timestamps** are signed time assertions, typically issued by a **Trusted Timestamp Authority (TSA)** using the **RFC 3161** Time-Stamp Protocol.
In Sigstore’s ecosystem, timestamping is used to provide **trusted time** for signatures, which can be important when reasoning about key compromise, certificate validity windows, or policy that depends on “when” an artifact was signed.

Sigstore integrates timestamping into **Cosign** verification workflows and provides a reference **timestamp-authority** service implementation.

## Overview

Sigstore’s “keyless” signing model commonly relies on short-lived signing identities (for example, via OpenID Connect) and transparency logs.
Timestamping is a complementary mechanism:

- A TSA produces a signed timestamp token asserting that a particular message imprint existed at (or before) a stated time.
- Verifiers can validate the TSA signature and certificate chain, and then treat the timestamp as a trusted input to policy.

Sigstore documentation describes timestamp support in Cosign and how TSAs are configured and verified.

## Components

### Cosign

**Cosign** is Sigstore’s signing and verification tool for container images and other artifacts.
Cosign can verify signatures and (when present) verify signed timestamps issued by a TSA.

See: Sigstore documentation on Cosign timestamp verification.

### Timestamp Authority (TSA)

A **Timestamp Authority** issues RFC 3161 timestamps.
Sigstore maintains an open-source timestamp authority service intended to be run by operators who want to provide trusted time.

Sigstore’s timestamp-authority repository describes the service as issuing RFC 3161 timestamps.

## Why timestamps matter (agent and automation context)

In autonomous agent systems, timestamping can support policies such as:

- **“Signed before” / “signed after” gates** for deployments.
- **Key compromise recovery** workflows (e.g., rejecting signatures after a compromise time).
- **Auditable build/release pipelines** where provenance, signing, and time are all verified.

Timestamp verification is typically used alongside other supply-chain controls (such as transparency logs and provenance attestations), rather than as a replacement.

## Verification (high-level)

At a high level, timestamp verification involves:

1. Checking that the timestamp token is syntactically valid for RFC 3161.
2. Verifying the TSA’s signature over the timestamp token.
3. Validating the TSA certificate chain and any configured trust roots.
4. Applying local policy to decide whether the timestamp is acceptable.

Implementation details and configuration options are described in Sigstore’s Cosign documentation.

## See also

- [Sigstore](https://www.sigstore.dev/)
- [Cosign](https://docs.sigstore.dev/cosign/)
- [Rekor](https://docs.sigstore.dev/logging/overview/)

## References

- Sigstore documentation: *Timestamps* (Cosign verification). https://docs.sigstore.dev/cosign/verifying/timestamps/
- Sigstore blog: *Trusted Time in Sigstore*. https://blog.sigstore.dev/trusted-time/
- GitHub: sigstore/timestamp-authority. https://github.com/sigstore/timestamp-authority
