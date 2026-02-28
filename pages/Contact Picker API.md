---
title: Contact Picker API
---

# Contact Picker API

The **Contact Picker API** is a proposed Web Platform API that enables a website to request *one-off* access to selected pieces of a user’s contact information through a user-agent mediated picker UI. The design emphasizes user control and consent by requiring an explicit user gesture and by limiting access to only the fields the user chooses to share.

## Overview

Many desktop and mobile platforms expose contact pickers that let users select recipients for messaging, email, or sharing flows. The Contact Picker API brings a similar interaction model to the web: instead of granting broad, persistent address-book access, sites request contacts *each time* they need them, and the browser presents a picker that makes the sharing action and the shared fields clear to the user.

The specification describes an API surface exposed on `navigator.contacts`, including a method for selecting contacts and a way to query which contact properties are supported by the user agent.

## Security and privacy model

Exposing contact information can reveal personally identifiable information (PII) about people other than the user. To mitigate this, the specification adopts a picker-based model and adds constraints intended to prevent silent or background access:

- **One-off access via a picker**: the user chooses which contacts and which fields to share for a given request.
- **User activation required**: the API is intended to be called in response to a user gesture (e.g., a button click).
- **Context restrictions**: the API is only available in a **top-level browsing context** and must be a **secure context**.

## API surface (high level)

The API is described as enabling sites to:

- Query supported properties (e.g., whether the user agent can provide `address` or `icon`).
- Request contacts with a specified set of fields, optionally allowing multiple selection.

### Example use cases

The specification includes example scenarios such as:

- Selecting email recipients for a webmail UI.
- Choosing a shipping or delivery address for a “send a gift” flow.
- Selecting a display name and icon for a social/sharing feature.

## Relationship to other standards

The Contact Picker API is referenced by related work that needs standardized contact/address component definitions beyond payment flows. For example, the Payment Request API work has discussed referencing address components defined in the Contact Picker API rather than defining them independently.

## See also

- [Payment Request API](./Payment%20Request%20API.md)
- [Payment Handler API](./Payment%20Handler%20API.md)

## References

- W3C (Editor’s Draft mirror): *Contact Picker API* (2024-03-20 ED). https://das.w3c.himor.in/ED-contact-picker-20240320.html
- MDN Web Docs: *Payment Request API* (notes the API’s relationship to payment flows and related specs). https://developer.mozilla.org/en-US/docs/Web/API/Payment_Request_API
- W3C (GitHub): *Payment Request API* (Candidate Recommendation Snapshot / editor’s draft text). https://w3c.github.io/payment-request/
