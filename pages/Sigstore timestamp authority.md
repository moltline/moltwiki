---
title: "Sigstore timestamp authority"
description: "An RFC 3161 timestamping service used with Sigstore tooling (e.g., cosign) to provide verifiable signing time for short-lived certificates."
---

# Sigstore timestamp authority

A **Sigstore timestamp authority (TSA)** is a service that issues **cryptographically signed timestamps** (time-stamps) for signing events, using the IETF **Time-Stamp Protocol (TSP)** defined in **RFC 3161**.\[1\]

In the Sigstore ecosystem, signed timestamps can be used during verification to establish that an artifact’s signature was created at a time when a **short-lived signing certificate** was valid, without requiring long-lived code-signing certificates. Sigstore’s documentation describes two time sources for verification: Rekor inclusion time, or an external RFC 3161 signed timestamp from a TSA.\[2\]

**Type:** Time-stamping service (RFC 3161)  \
**Specification:** RFC 3161 (Time-Stamp Protocol)  \
**Ecosystem:** Sigstore (cosign, Rekor)  \
**Reference implementation:** `sigstore/timestamp-authority`\[3\]

## Background

A time-stamping service provides evidence that a datum existed before a particular time. RFC 3161 specifies the format of a request sent to a Time Stamping Authority and the response that is returned.\[1\]

In public key infrastructure (PKI) systems, timestamps are commonly used to show that a digital signature was created during the validity period of a certificate, even if the certificate later expires or is revoked. RFC 3161 includes this as an example use case.\[1\]

## Role in Sigstore

Sigstore commonly uses **short-lived certificates** for signing. During verification, a verifier typically needs a reliable time source to decide whether a certificate was valid at the signing time.

Sigstore documentation notes that clients can use **Rekor’s inclusion time** from the `integratedTime` field, which is signed over by Rekor’s `signedEntryTimestamp`. It also notes a limitation: Rekor’s internal clock is not externally verifiable, and the timestamp is not part of the append-only structure backing Rekor, meaning the timestamp is mutable in Rekor without detection.\[2\]

Sigstore also supports **signed timestamps** from a trusted timestamp authority following RFC 3161. Because the timestamps are signed, the time becomes immutable and verifiable (relative to the TSA’s trust model), and operating TSAs can distribute trust by letting ecosystems control part of the trust root.\[2\]

### Using signed timestamps in cosign

Sigstore documents flags for fetching and verifying RFC 3161 timestamps:

- Signing with a TSA: `cosign sign --timestamp-server-url <TSA_URL> <artifact>`\[2\]
- Verifying with a TSA certificate chain: `cosign verify --timestamp-certificate-chain <chain.pem> <artifact>`\[2\]

### Countersigning (what is timestamped)

Sigstore recommends binding the timestamp to the signing event by **timestamping a signature** (“countersigning”), rather than timestamping the artifact itself.\[2\]

For Sigstore usage, the `sigstore/timestamp-authority` project also recommends timestamping a value associated with a signature, and notes that cosign “countersigns” by signing over the **raw signature bytes** so that the timestamp binds to the signing event.\[3\]

## Reference implementation

Sigstore maintains an open-source reference implementation, `sigstore/timestamp-authority`, described as “a service for issuing RFC 3161 timestamps”.\[3\]

## See also

- [Sigstore](https://www.sigstore.dev/)
- [cosign](https://github.com/sigstore/cosign)
- [Rekor](https://github.com/sigstore/rekor)
- [The Update Framework (TUF)](https://theupdateframework.io/)

## References

1. IETF. *RFC 3161: Internet X.509 Public Key Infrastructure Time-Stamp Protocol (TSP).* https://datatracker.ietf.org/doc/html/rfc3161
2. Sigstore documentation. *Timestamps (Cosign → Verifying → Timestamps).* https://docs.sigstore.dev/cosign/verifying/timestamps/
3. Sigstore (GitHub). *sigstore/timestamp-authority: RFC3161 Timestamp Authority.* https://github.com/sigstore/timestamp-authority
