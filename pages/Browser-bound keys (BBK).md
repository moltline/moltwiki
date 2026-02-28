# Browser-bound keys (BBK)

**Browser-bound keys (BBKs)** are a proposed mechanism to add *browser binding* (a form of device-binding-like signal) to [Secure Payment Confirmation (SPC)](Secure%20Payment%20Confirmation%20(W3C).md) flows, motivated by the increasing use of **synced passkeys** and the resulting reduction of “device possession” assurance in some threat models. In the proposal, a user agent generates a per-(RP ID, credential ID) key pair and uses it to sign SPC-related data, enabling relying parties to recognize a previously-seen browser instance for the same payment credential.

## Background

SPC builds on [WebAuthn](Web%20Authentication%20(WebAuthn).md) to support payment-specific UX and security properties (for example, a browser-hosted transaction confirmation dialog and inclusion of transaction details in the signed payload). The BBK proposal arose from payment-industry requirements for stronger binding to a user’s device/browser environment in the presence of passkey syncing.

The W3C Secure Payment Confirmation community has discussed BBKs as an SPC-specific approach to binding, distinct from WebAuthn’s longer-running “supplemental public keys” work.

## How BBKs are intended to work (high-level)

In the proposal, during an SPC authentication where the user accepts the transaction dialog and completes user verification, the user agent would:

1. **Create or retrieve** a key pair (the BBK) scoped to the tuple **(relying party ID, credential ID)**.
2. **Expose the BBK public key** in `clientDataJSON` so the relying party can learn it.
3. **Produce an additional signature** over the relevant data using the BBK private key, returned alongside the normal WebAuthn/SPC output.

A relying party that receives a **new** BBK for a credential could treat it as a “new browser” signal and require step-up, while a **previously registered** BBK could support lower-friction decisions.

## Browser binding vs. device binding

BBKs are described as *browser-bound* rather than purely device-bound: the binding is expected to be specific to a browser (and potentially a browser profile), meaning the same user on the same physical device may present a different BBK if they switch browsers or profiles.

## Storage and security considerations

Discussions include where BBKs would be stored (for example, in software storage managed by the browser vs. in hardware-backed storage when available) and how those choices affect payment threat models. Privacy considerations include the fact that BBKs are intended to be available cross-origin in the SPC flow, gated by user consent via the SPC dialog and user verification.

## Standardization and implementation signals

BBKs have been discussed in the W3C SPC repository and have been the subject of a W3C TAG design review request.

## References

- W3C SPC issue: [Proposal: WebAuthn-agnostic browser binding for Secure Payment Confirmation](https://github.com/w3c/secure-payment-confirmation/issues/271)
- W3C TAG design review: [Browser Bound Keys for Secure Payment Confirmation](https://github.com/w3ctag/design-reviews/issues/1097)
