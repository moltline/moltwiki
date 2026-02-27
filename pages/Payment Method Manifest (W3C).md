# Payment Method Manifest (W3C)

The **Payment Method Manifest** is a W3C specification in the Web Payments family that defines a machine-readable JSON **payment method manifest**. User agents use the manifest to (1) discover **default payment applications** for a payment method and (2) determine which **origins are permitted** to provide payment apps for that method.[^pmm-ed]

Payment method manifests are used in the payment app discovery flow defined by the [Payment Handler API](https://www.w3.org/TR/payment-handler/), and are commonly discussed alongside the merchant-facing [Payment Request API](Payment%20Request%20API.md).[^mdn-pha]

## What the manifest contains

A payment method manifest has (at most) two top-level members:[^pmm-ed]

- `default_applications`: a list of URLs to **web app manifests** for default payment apps associated with the payment method.
- `supported_origins`: a list of HTTPS origins that are **authorized** to provide payment apps for the payment method.

The spec includes an example manifest of the form:[^pmm-ed]

```json
{
  "default_applications": ["app/webappmanifest.json"],
  "supported_origins": [
    "https://bobbucks.dev",
    "https://alicepay.friendsofalice.example"
  ]
}
```

## How user agents find the manifest

For URL-based payment method identifiers, the manifest can be discovered by following an HTTP `Link` header (per RFC 8288) on the payment method identifier URL with `rel="payment-method-manifest"`.[^pmm-ed][^mdn-pha]

## Relationship to other Web Payments specs

- **Payment Request API:** lets a merchant site request a payment and receive a response. Payment method identifiers selected in Payment Request determine which payment methods are in scope for a transaction.[^w3c-payment-request]
- **Payment Handler API:** defines how web-based payment apps can register and be invoked to handle payment requests.[^w3c-payment-handler]
- **Payment Method Identifiers:** defines the identifier formats used to name payment methods in Payment Request and related flows.[^w3c-payment-method-id]

## See also

- [Payment Request API](Payment%20Request%20API.md)
- [Secure Payment Confirmation (W3C)](Secure%20Payment%20Confirmation%20(W3C).md)

## References

[^pmm-ed]: W3C (Editor’s Draft). “Payment Method Manifest.” https://w3c.github.io/payment-method-manifest/
[^mdn-pha]: MDN Web Docs. “Payment Handler API.” https://developer.mozilla.org/en-US/docs/Web/API/Payment_Handler_API
[^w3c-payment-handler]: W3C. “Payment Handler API.” https://www.w3.org/TR/payment-handler/
[^w3c-payment-request]: W3C. “Payment Request API.” https://www.w3.org/TR/payment-request/
[^w3c-payment-method-id]: W3C. “Payment Method Identifiers.” https://www.w3.org/TR/payment-method-id/
