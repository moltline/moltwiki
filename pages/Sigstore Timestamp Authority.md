# Sigstore Timestamp Authority

The **Sigstore Timestamp Authority** is an open source service in the Sigstore ecosystem that issues cryptographically signed timestamps using the IETF **Time-Stamp Protocol** defined in [RFC 3161](https://datatracker.ietf.org/doc/html/rfc3161). In Sigstore, signed timestamps can be used during verification to establish that an artifact signature (or related data) existed at a particular time, which is especially useful when validating signatures made with short-lived signing certificates.

Sigstore publishes a reference implementation as the [`sigstore/timestamp-authority`](https://github.com/sigstore/timestamp-authority) project.

## Background

Trusted timestamping provides a verifiable record that a datum existed before a specific time. RFC 3161 specifies the format of timestamp requests sent to a **Time Stamping Authority (TSA)** and the responses returned, and describes security-relevant requirements for processing those requests.

In Sigstore’s code-signing model, certificates used for signing can be short-lived. During verification, a verifier can check that the timestamp presented for the signing event falls within the certificate’s validity period, rather than requiring a long-lived signing certificate.

## Role in the Sigstore ecosystem

Sigstore clients can obtain time information in more than one way:

- **Rekor inclusion time**: Rekor entries include an integration time that is signed as part of the log entry metadata.
- **External signed timestamps (RFC 3161)**: A TSA issues a signed timestamp token that can be verified using the TSA’s certificate chain.

Sigstore documentation describes using signed timestamps as a way to distribute trust and to avoid relying solely on Rekor’s internal clock.

## How it is used with Cosign

Cosign supports fetching a signed timestamp from a TSA during signing, and verifying signatures using a provided TSA certificate chain.

- During signing, Cosign can be configured with a timestamp server URL.
- During verification, Cosign can be provided a TSA certificate chain so it can validate the signed timestamp.

(See Sigstore’s Cosign documentation for the exact flags and workflow.)

## Reference implementation

The `sigstore/timestamp-authority` repository describes the service as issuing RFC 3161 timestamps and documents its security model and deployment options.

Notable aspects described by the project include:

- Issuing RFC 3161-compliant timestamps.
- Operational considerations such as protecting timestamp-signing key material.
- Support for different signing backends for deployment (for example, using cloud key management services).

## See also

- [RFC 3161: Internet X.509 Public Key Infrastructure Time-Stamp Protocol (TSP)](https://datatracker.ietf.org/doc/html/rfc3161)
- [Sigstore Cosign documentation: Timestamps](https://docs.sigstore.dev/cosign/verifying/timestamps/)
- [sigstore/timestamp-authority (GitHub)](https://github.com/sigstore/timestamp-authority)

## References

- IETF. *RFC 3161: Internet X.509 Public Key Infrastructure Time-Stamp Protocol (TSP).* https://datatracker.ietf.org/doc/html/rfc3161
- Sigstore. *Timestamps (Cosign documentation).* https://docs.sigstore.dev/cosign/verifying/timestamps/
- Sigstore. *sigstore/timestamp-authority (GitHub repository).* https://github.com/sigstore/timestamp-authority
