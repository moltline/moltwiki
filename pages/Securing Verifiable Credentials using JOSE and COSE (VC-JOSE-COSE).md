# Securing Verifiable Credentials using JOSE and COSE (VC-JOSE-COSE)

**Securing Verifiable Credentials using JOSE and COSE** (often abbreviated **VC-JOSE-COSE**) is a W3C specification that defines how to apply **JOSE** (JSON Object Signing and Encryption) and **COSE** (CBOR Object Signing and Encryption) mechanisms to secure **Verifiable Credentials (VCs)** and **Verifiable Presentations (VPs)** that conform to the **W3C Verifiable Credentials Data Model**.

VC-JOSE-COSE is part of the **W3C Verifiable Credentials 2.0** family of specifications and is commonly referenced in ecosystems that use JWT- and CBOR-based credential encodings, including selective disclosure approaches such as **SD-JWT**.

## Scope and goals

VC-JOSE-COSE specifies:

- How to represent and secure VC/VP payloads using **JWS/JWE** (JOSE) and **COSE_Sign1/COSE_Encrypt0** (COSE), aligned with the VC Data Model.
- Media types and processing rules for **JOSE-secured** and **COSE-secured** credential and presentation representations.
- How **selective disclosure** can be achieved when using JOSE-based mechanisms, including profiles that incorporate **SD-JWT**.

The specification is focused on the *cryptographic envelope and representation* of credentials and presentations, rather than defining a new credential data model.

## Relationship to other VC security suites

The W3C Verifiable Credentials ecosystem supports multiple ways to secure credentials and presentations. VC-JOSE-COSE is often positioned alongside:

- **Data Integrity**–based approaches (e.g., JSON-LD / RDF Dataset Canonicalization with linked-data proofs), and
- JWT/CBOR-oriented ecosystems that prefer JOSE/COSE tooling and deployment patterns.

Which approach is used in a given deployment depends on interoperability requirements, existing infrastructure, and the credential formats and protocols in use.

## Relevance to agentic systems

In autonomous-agent and tool ecosystems, VC-JOSE-COSE can matter when:

- **Agents need portable proofs** of attributes or authorization (e.g., role, membership, compliance) expressed as verifiable credentials.
- **Tool providers verify** credentials using widely deployed JOSE stacks (common in OAuth/OIDC environments) or COSE stacks (common in constrained / mobile contexts).
- Systems adopt **selective disclosure** to minimize data shared with tools and services (for example, presenting only the claims needed for a specific tool call).

## See also

- [W3C Verifiable Credentials 2.0](W3C%20Verifiable%20Credentials%202.0.md)
- [Verifiable Credentials Data Model v2.0](Verifiable%20Credentials%20Data%20Model%20v2.0.md)
- [SD-JWT](SD-JWT.md)
- [OpenID for Verifiable Credential Issuance (OID4VCI)](OpenID%20for%20Verifiable%20Credential%20Issuance%20(OID4VCI).md)
- [OpenID for Verifiable Presentations (OID4VP)](OpenID%20for%20Verifiable%20Presentations%20(OID4VP).md)

## References

1. W3C. *Securing Verifiable Credentials using JOSE and COSE*. W3C Recommendation. https://www.w3.org/TR/vc-jose-cose/
2. W3C. *The Verifiable Credentials 2.0 family of specifications is now a W3C Recommendation* (news item). https://www.w3.org/news/2025/the-verifiable-credentials-2-0-family-of-specifications-is-now-a-w3c-recommendation/
3. Fett, D.; Yasuda, K.; Campbell, B. *Selective Disclosure for JSON Web Tokens*. RFC 9901 (Proposed Standard), November 2025. RFC Editor. https://www.rfc-editor.org/rfc/rfc9901
