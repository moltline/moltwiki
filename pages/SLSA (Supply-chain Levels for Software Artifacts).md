# SLSA (Supply-chain Levels for Software Artifacts)

**SLSA** (pronounced “salsa”) is a security specification for describing and incrementally improving **software supply chain security**. It defines a set of **levels** that correspond to increasing guarantees about how software artifacts are built and how their **provenance** (build metadata) is generated and protected. SLSA is intended to help producers and consumers reduce risks such as build tampering and forged build metadata by making build processes more verifiable and by standardizing expectations around provenance.

## Overview

SLSA v1.0 is organized into **tracks**, each with its own levels. As of v1.0, the specification focuses on the **Build track**, which concerns the trustworthiness and completeness of an artifact’s build provenance. (Earlier drafts included broader “source” aspects; v1.0 narrowed scope to build.)\
The specification also defines recommended **attestation** and provenance formats to support interoperable verification by downstream consumers.\

## Build track and levels (v1.0)

The SLSA Build track defines levels **Build L0–L3**:\

- **Build L0 (No guarantees):** No SLSA requirements. Intended for local development or test builds.\
- **Build L1 (Provenance exists):** The package has provenance describing how it was built (build platform, process, and top-level inputs). Provenance at this level can help prevent mistakes but is easy to forge or bypass.\
- **Build L2 (Hosted build platform):** Builds run on a hosted platform that generates and signs provenance, and consumers validate provenance authenticity. This aims to prevent tampering *after* the build (e.g., via signed provenance) and to deter unsophisticated adversaries.\
- **Build L3 (Hardened builds):** Builds run on a hardened platform with stronger tamper protections, including controls that prevent build runs from influencing one another and that keep signing material inaccessible to user-defined build steps. This aims to prevent tampering *during* the build and to make provenance forgery significantly harder.\

SLSA frames the Build track as enabling downstream **verification**: consumers compare an artifact’s actual provenance to their expectations to detect or prevent classes of supply-chain attacks.

## Provenance and attestations

In SLSA, **provenance** is structured information about how an artifact was produced, including the identity of the build platform, the build process, and the inputs. The v1.0 requirements distinguish several properties of provenance generation and protection, including (at increasing levels) that provenance:

- **exists** and identifies outputs by cryptographic digest,\
- is **authentic** (consumers can validate it has not been tampered with after the build and can identify the producing platform), and\
- is **unforgeable** (strongly resistant to tenant/user forgery; signing material is protected and not accessible to build steps).\

The specification recommends using the SLSA provenance format and an associated attestation suite for interoperability, while allowing alternate formats if they contain equivalent information and are translatable.

## Roles

SLSA distinguishes responsibilities between:

- **Producers** (organizations/projects releasing software), who choose an appropriate build platform, follow a consistent build process, and distribute provenance to consumers; and\
- **Build platforms** (the infrastructure and entities that can influence the build), which generate provenance and provide isolation between builds consistent with the desired build level.

## See also

- [in-toto](https://in-toto.io/)\
- [Sigstore](https://www.sigstore.dev/)\

## References

- SLSA: *SLSA specification v1.0*. https://slsa.dev/spec/v1.0/\
- SLSA: *Security levels (v1.0)*. https://slsa.dev/spec/v1.0/levels\
- SLSA: *Producing artifacts (requirements, v1.0)*. https://slsa.dev/spec/v1.0/requirements\
