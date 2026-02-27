---
title: "RFC Errata"
description: "How RFC errata work at the RFC Editor, including statuses, how to read an erratum, and how to cite errata in engineering work."
---

## What it is

**RFC errata** are post-publication corrections or clarifications reported against an RFC and tracked by the **RFC Editor** in an **Errata Report** database. Errata are commonly used to fix **editorial mistakes** (typos, incorrect terms, broken references) and to flag potential **technical issues** discovered after publication.

The canonical index is the RFC Editor’s errata search for a given RFC number (e.g., the errata page for RFC 9449). https://www.rfc-editor.org/errata/rfc9449

## Why it matters

- **Engineering accuracy**: Implementations often rely on a precise reading of normative text. A small wording error (e.g., using the wrong OAuth role term) can cause confusion or mis-implementation.
- **Standards hygiene**: Errata provide a lightweight way to correct issues without immediately publishing a new RFC.
- **Citation trail**: In design docs and security reviews, citing a verified erratum can justify a particular interpretation or correction.

## Where errata live

The RFC Editor maintains:

- An **errata landing page per RFC** (e.g., `https://www.rfc-editor.org/errata/rfcNNNN`).
- Individual **erratum records** with stable IDs (e.g., `eid7646`).
- Definitions of **statuses** and **types**.

Status definitions: https://www.rfc-editor.org/errata-definitions/

## Errata types

Errata are categorized by **type**:

- **Editorial**: Non-substantive fixes (terminology, spelling, formatting, broken links, etc.).
- **Technical**: Substantive changes that may affect protocol behavior or interpretation.

In practice, “editorial” does not mean “unimportant”: an editorial erratum may still remove ambiguity that affects implementers.

## Errata statuses (what they mean)

The RFC Editor uses multiple statuses. The most commonly referenced are:

- **Reported**: Submitted but not yet reviewed/approved.
- **Verified**: Confirmed as correct (i.e., the erratum is accepted as an error in the RFC).
- **Rejected**: Not accepted as an error.
- **Held for Document Update**: Acknowledged, but intended to be addressed in a future revision/update rather than applied directly.

See the full definitions: https://www.rfc-editor.org/errata-definitions/

## How to read an erratum record

An erratum record typically includes:

- **Errata ID** (e.g., `7646`)
- **Status** (Reported / Verified / etc.)
- **Type** (Editorial / Technical)
- The affected **RFC and section**
- The original text (“says”) and corrected text (“It should say”)
- Dates and verifier information

Example (RFC 9449, Errata ID 7646): the erratum corrects the phrase “authentication server” to “authorization server” in Section 4.2 in the context of a `DPoP-Nonce` header. https://www.rfc-editor.org/errata/eid7646

## Using errata in implementation work

Practical guidance:

- Prefer **Verified** errata when you need to justify a correction in code or documentation.
- Treat **Reported** errata as *signals*, not authoritative corrections.
- When writing docs, cite both the RFC and the erratum record (by `eidXXXX`) so readers can locate the exact correction.

## Relationship to other IETF change mechanisms

Errata are not the same as publishing an updated specification:

- **Internet-Drafts** and **bis** documents are used for ongoing work and eventual replacement/update RFCs.
- Errata are a post-publication tracking mechanism; they can inform future updates and may be incorporated later.

## Sources

- RFC Editor errata definitions: https://www.rfc-editor.org/errata-definitions/
- RFC Editor errata record for RFC 9449 (Errata index): https://www.rfc-editor.org/errata/rfc9449
- RFC Editor erratum record `eid7646` (RFC 9449): https://www.rfc-editor.org/errata/eid7646
- RFC 9449 (DPoP): https://www.rfc-editor.org/rfc/rfc9449
