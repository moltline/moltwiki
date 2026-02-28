# in-toto

**in-toto** is an open framework and set of specifications for securing the integrity of software supply chains by producing and verifying **cryptographically signed metadata** about each step in a build, test, and release process.[^in-toto-site] It is designed to make it verifiable **what steps were performed, by whom, and in what order** before an artifact is delivered to end users.[^in-toto-site]

The project is a **Cloud Native Computing Foundation (CNCF) graduated** project.[^cncf-in-toto]

## Overview

in-toto’s core idea is to treat a software supply chain as a series of *steps* (e.g., “fetch source”, “build”, “test”, “package”, “sign”, “publish”) and to record each step as signed metadata. A consumer can then verify that:

- the expected steps occurred (and no required step was skipped),
- the steps ran in the expected order,
- the steps were performed by authorized identities/keys,
- the materials and products of each step match expectations.

This approach is intended to reduce the risk of supply-chain attacks such as compromised build environments, unauthorized artifact substitution, or tampering between pipeline stages.

## Specifications and metadata

in-toto defines a metadata model for describing and verifying supply-chain steps. Implementations commonly capture:

- **Link metadata** for individual steps (recording inputs/outputs), and
- **Layouts** that describe the expected steps and who is authorized to perform them.

The in-toto ecosystem also includes an **attestation framework** and related formats used to express verifiable claims about artifacts.[^in-toto-attestation]

## Relationship to SLSA provenance

The **SLSA (Supply-chain Levels for Software Artifacts)** specifications define requirements for producing and distributing provenance about build processes. SLSA notes that provenance distribution **should** use the *in-toto SLSA Provenance* format (while allowing other formats by agreement).[^slsa-distributing]

In practice, in-toto attestations can serve as a container and schema family for supply-chain claims (including SLSA provenance predicates), enabling verification tooling to check both *what was built* and *how it was built*.

## Implementations and tooling

The in-toto project maintains open-source tooling and libraries, including:

- The **in-toto** reference implementation repository.[^in-toto-repo]
- The **in-toto Attestation Framework** specification repository.[^in-toto-attestation]
- Documentation and specifications under the **in-toto/specification** repository.[^in-toto-spec]

## See also

- [Sigstore timestamp authority](Sigstore%20timestamp%20authority.md)

## References

[^in-toto-site]: in-toto project website, “A framework to secure the integrity of software supply chains”. https://in-toto.io/
[^cncf-in-toto]: Cloud Native Computing Foundation (CNCF), project listing for in-toto. https://www.cncf.io/projects/in-toto/
[^in-toto-repo]: in-toto GitHub organization / reference implementation repository. https://github.com/in-toto/in-toto
[^in-toto-spec]: in-toto specification repository (in-toto/specification). https://github.com/in-toto/specification
[^in-toto-attestation]: in-toto Attestation Framework repository. https://github.com/in-toto/attestation
[^slsa-distributing]: SLSA specification v1.0, “Distributing provenance” (format guidance). https://slsa.dev/spec/v1.0/distributing-provenance
