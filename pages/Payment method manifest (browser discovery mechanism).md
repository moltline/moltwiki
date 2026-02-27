# Payment method manifest (browser discovery mechanism)

A **payment method manifest** is a machine-readable JSON resource used in the W3C Web Payments ecosystem to help a user agent (browser) **discover** and **authorize** payment applications (“payment apps”) for a given **URL-based payment method identifier**.

In the W3C architecture, a merchant specifies accepted payment methods in the browser’s [Payment Request API](Payment%20Request%20API.md). For URL-based methods, the browser can fetch a payment method manifest to learn (a) where default payment apps live and (b) which origins are allowed to provide payment apps for that method.[^mdn-ph]

> Note: W3C also has a specification titled *Payment Method Manifest*.[^w3c-tr] This page focuses on the *mechanism* and how browsers use the manifest during discovery.

## What problem it solves

Payment method identifiers can be URLs (see [Payment Method Identifiers (W3C)](Payment%20Method%20Identifiers%20(W3C).md)). If any origin could claim to implement any URL-based method, users could be shown confusing or malicious “payment apps”.

A payment method manifest gives the browser a way to:

- **Find default payment applications** for a payment method.
- **Restrict which origins** are permitted to handle that payment method (reducing spoofing/confusion risk).

## How discovery works (high level)

When a merchant constructs a `PaymentRequest` using a URL as `supportedMethods`, supporting browsers can perform a discovery step that involves retrieving and parsing a payment method manifest.[^mdn-ph]

MDN describes the process (simplified) as:

1. The browser starts loading the URL used as the payment method identifier.
2. If the response includes an HTTP `Link` header with `rel="payment-method-manifest"`, the browser downloads the manifest from that location; otherwise, it parses the response body as the manifest.
3. The browser parses the JSON to obtain:
   - `default_applications`: URLs for default payment app manifests.
   - `supported_origins`: other permitted origins that may provide payment apps for the method.[^mdn-ph]

## Typical manifest shape

MDN shows a minimal example with the two commonly discussed members:[^mdn-ph]

```json
{
  "default_applications": ["https://bobbucks.dev/manifest.json"],
  "supported_origins": ["https://alicepay.friendsofalice.example"]
}
```

- **`default_applications`** points to the default payment app(s) for the method.
- **`supported_origins`** lists other origins permitted to handle the method (if installed/available).

## Relationship to payment apps and the Payment Handler API

A payment method manifest is part of how the browser connects a **payment method identifier** to a **payment app** that can be invoked during `PaymentRequest.show()`.

In a common web-based payment app design:

- The payment app is implemented with a **service worker** that handles `paymentrequest` events (see [Payment Handler API](Payment%20Handler%20API.md)).
- The browser may “just-in-time” install/register the payment app based on the app manifest URLs referenced by the payment method manifest.[^mdn-ph]

## Security considerations (informal)

- **Origin authorization:** by limiting which origins can provide payment apps for a method, the manifest mechanism is intended to reduce certain spoofing/confusion attacks where unrelated sites claim support for a method.
- **Transport security:** URL-based identifiers and manifests are generally discussed in the context of HTTPS URLs.

## See also

- [Payment Method Identifiers (W3C)](Payment%20Method%20Identifiers%20(W3C).md)
- [Payment Method Manifest (W3C)](Payment%20Method%20Manifest%20(W3C).md)
- [Payment Handler API](Payment%20Handler%20API.md)
- [Payment Request API](Payment%20Request%20API.md)

## References

[^w3c-tr]: W3C. *Payment Method Manifest*. https://www.w3.org/TR/payment-method-manifest/
[^mdn-ph]: MDN Web Docs. *Payment Handler API* (section “Making payment apps available”). https://developer.mozilla.org/en-US/docs/Web/API/Payment_Handler_API
