# Verifiable Credential Status List 2021

**Verifiable Credential Status List 2021** (often shortened to **Status List 2021**) is a specification from the W3C Verifiable Credentials ecosystem that describes a **privacy-preserving** and **space-efficient** way to publish status information (for example, whether a Verifiable Credential has been **revoked** or **suspended**) using a **compressed bitstring**.

It was published as a W3C **Community Group Final Report** and later evolved into the W3C Verifiable Credentials Working Group’s **Bitstring Status List** specification.

## Overview

Many Verifiable Credential (VC) deployments need a way for verifiers to check whether a credential is still valid (not revoked or suspended). A naive approach is to publish a unique status URL per credential. The Status List 2021 design instead groups many credentials into a single list to improve privacy and reduce bandwidth.

At a high level:

- An **issuer** maintains a status list covering many credentials.
- Each issued VC includes a `credentialStatus` entry that points to the status list and indicates an **index** into the list.
- The list is represented as a **bitstring** that can be efficiently compressed (for example, because most credentials are expected to remain in the “valid” state).

## Privacy motivation

Status checks can leak metadata. If each credential has a unique status URL, the status service can potentially correlate:

- which credential is being checked,
- when it is checked,
- and who is checking it.

By placing many credentials’ statuses into a shared list, Status List 2021 aims to provide **group privacy** and make correlation harder, while remaining compatible with web-scale distribution and caching.

## Relationship to Bitstring Status List

Status List 2021 is closely related to (and is a predecessor of) **Bitstring Status List**:

- Status List 2021 was published under the W3C Credentials Community Group.
- The Verifiable Credentials Working Group later standardized a similar approach as **Bitstring Status List** (W3C Recommendation), with updates and clarifications.

In practice, many discussions, implementations, and documentation now point to Bitstring Status List as the current W3C-track specification.

## References

- W3C Credentials Community Group. *Status List 2021* (Community Group Final Report, 2023-01-02). https://www.w3.org/community/reports/credentials/CG-FINAL-vc-status-list-2021-20230102/
- W3C Verifiable Credentials Working Group. *Bitstring Status List* (specification repository / editor’s draft). https://github.com/w3c/vc-bitstring-status-list
- w3c-ccg/vc-status-list-2021 (archived). *vc-status-list-2021* repository. https://github.com/w3c-ccg/vc-status-list-2021
