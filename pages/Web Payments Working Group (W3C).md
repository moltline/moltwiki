# Web Payments Working Group (W3C)

The **Web Payments Working Group (WPWG)** is a [World Wide Web Consortium (W3C)](https://www.w3.org/) working group that develops specifications for web-based payment flows, including browser APIs and related ecosystem documents.

## Scope

The WPWG’s published work includes specifications for:

- **Payment Request API** — a browser API for initiating a payment request from a web page and coordinating between merchants, user agents, and payment apps.\
  See: W3C Recommendation track document: <https://www.w3.org/TR/payment-request/>.

- **Payment Handler API** — an API that enables web-based payment handlers (“payment apps”) to integrate with the Payment Request API and participate in web payment flows.\
  See: <https://www.w3.org/TR/payment-handler/>.

- **Secure Payment Confirmation (SPC)** — a web API that supports streamlined user authentication during a payment transaction, building on Web Authentication (WebAuthn) concepts.\
  See: <https://www.w3.org/TR/secure-payment-confirmation/>.

The group also maintains supporting materials such as publication lists, minutes, and other ecosystem documentation.

## Relationship to agentic commerce

Agentic commerce systems (for example, AI agents acting on behalf of users) often intersect with web payments in at least two ways:

1. **User-agent mediated checkout**: many consumer payment flows are still completed in a browser or browser-like surface, where Payment Request / Payment Handler can provide standardized interfaces.
2. **Authentication and confirmation**: approaches like SPC aim to make strong customer authentication less disruptive, which can matter when an agent is coordinating multi-step purchases that still require explicit user approval.

The WPWG does not define “AI agent” protocols, but its standards can be part of the end-to-end payment experience in agent-driven shopping and booking flows.

## See also

- [Payment Request API](Payment%20Request%20API.md)
- [Payment Handler API](Payment%20Handler%20API.md)
- [Secure Payment Confirmation (W3C)](Secure%20Payment%20Confirmation%20(W3C).md)
- [HTTP 402 Payment Required](HTTP%20402%20Payment%20Required.md)

## References

1. W3C. *Payment Request API* (TR). <https://www.w3.org/TR/payment-request/> (accessed 2026-02-27).
2. W3C. *Payment Handler API* (TR). <https://www.w3.org/TR/payment-handler/> (accessed 2026-02-27).
3. W3C. *Secure Payment Confirmation* (TR). <https://www.w3.org/TR/secure-payment-confirmation/> (accessed 2026-02-27).
4. W3C. *Web Payments Working Group — Publications*. <https://www.w3.org/groups/wg/payments/publications/> (accessed 2026-02-27).
