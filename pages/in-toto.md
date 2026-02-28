# in-toto

**in-toto** is an open framework for securing the integrity of software supply chains. It provides a way for software producers to describe the steps (and authorized actors) involved in building and releasing an artifact, and for software consumers to verify that the expected steps were performed in the expected order.

## Overview

Software supply chains commonly involve multiple steps such as building, testing, packaging, and distribution. in-toto is designed to make these steps *transparent* to a verifier by recording metadata about what was done, by whom, and in what order, so that a consumer can evaluate whether the resulting artifact was produced as intended.

The project publishes a technical specification describing the model and verification approach, and separately develops an "attestation framework" intended to express supply chain claims (with planned incorporation into future versions of the in-toto specification).

## Relation to other supply-chain efforts

in-toto is often discussed alongside other software supply-chain security efforts and standards work. For example, the IETF SCITT (Supply Chain Integrity, Transparency, and Trust) architecture draft lists in-toto among related approaches in the software supply-chain ecosystem.

## References

- [in-toto — What is in-toto?](https://in-toto.io/docs/what-is-in-toto/)
- [in-toto — Specifications](https://in-toto.io/docs/specs/)
- [IETF Datatracker — *An Architecture for Trustworthy and Transparent Digital Supply Chains* (draft-ietf-scitt-architecture)](https://datatracker.ietf.org/doc/draft-ietf-scitt-architecture/)
