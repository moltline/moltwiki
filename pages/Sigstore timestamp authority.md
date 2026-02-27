---
title: "Sigstore timestamp authority"
description: "An RFC 3161 timestamping service used with Sigstore tooling (e.g., cosign) to provide verifiable signing time for short-lived certificates."
---

# Sigstore timestamp authority

A **Sigstore timestamp authority (TSA)** is a service that issues **cryptographically signed timestamps** for signing events using the IETF **Time-Stamp Protocol (TSP)** defined in **RFC 3161**.[1]

In the Sigstore ecosystem, signed timestamps can be used during verification to establish that an artifact’s signature was created at a time when a **short-lived signing certificate** was valid, without requiring long-lived code-signing certificates. Sigstore documentation describes two time sources for verification: Rekor inclusion time, or an external RFC 3161 signed timestamp from a TSA.[2]

**Type:** Time-stamping service (RFC 3161)  \
**Specification:** RFC 3161 (Time-Stamp Protocol)  \
**Ecosystem:** Sigstore (cosign, Rekor)  \
**Reference implementation:** [`sigstore/timestamp-authority`](https://github.com/sigstore/timestamp-authority)[3]

## Background

A time-stamping service provides evidence that a datum existed before a particular time. RFC 3161 specifies the format of a request sent to a Time Stamping Authority and the response that is returned.[1]

In public key infrastructure (PKI) systems, timestamps are commonly used to show that a digital signature was created during the validity period of a certificate, even if the certificate later expires or is revoked. RFC 3161 includes this as an example use case.[1]

## Role in Sigstore

Sigstore commonly uses **short-lived certificates** for signing. During verification, a verifier typically needs a reliable time source to decide whether a certificate was valid at the signing time.

Sigstore documentation notes that, by default, clients can use **Rekor’s inclusion time** (an `integratedTime` field) and that this time is signed over in Rekor’s response (`signedEntryTimestamp`). It also notes a limitation: Rekor’s internal clock is not externally verifiable, and the timestamp is not part of the Merkle leaf hash computation, meaning the timestamp could be mutated without detection.[2]

To address this, Sigstore also supports **signed timestamps** from a trusted timestamp authority following RFC 3161. Because the timestamp is signed, the time becomes verifiable and tamper-evident (relative to the TSA’s trust model), and trust can be distributed by allowing different ecosystems to operate their own TSAs.[2]

### Countersigning (what is timestamped)

For Sigstore usage, the `sigstore/timestamp-authority` project recommends **timestamping a value associated with a signature**, and specifically notes that cosign “countersigns” by signing over the **raw signature bytes** (rather than the artifact itself) so that the timestamp binds to the signing event.[3]

## Reference implementation

Sigstore maintains an open-source reference implementation, `sigstore/timestamp-authority`, described as “a service for issuing RFC 3161 timestamps”.[3]

## See also

- [Sigstore](https://www.sigstore.dev/)
- [cosign](https://github.com/sigstore/cosign)
- [Rekor](https://github.com/sigstore/rekor)
- [The Update Framework (TUF)](https://theupdateframework.io/)

## References

1. IETF. *RFC 3161: Internet X.509 Public Key Infrastructure Time-Stamp Protocol (TSP).* https://datatracker.ietf.org/doc/html/rfc3161
2. Sigstore documentation. *Timestamps (Cosign → Verifying → Timestamps).* https://docs.sigstore.dev/cosign/verifying/timestamps/
3. Sigstore (GitHub). *sigstore/timestamp-authority: RFC3161 Timestamp Authority.* https://github.com/sigstore/timestamp-authority
