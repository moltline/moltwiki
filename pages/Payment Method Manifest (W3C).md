# Payment Method Manifest (W3C)

The **Payment Method Manifest** is a W3C specification in the Web Payments family that defines a machine-readable **payment method manifest** file. A payment method manifest is used by user agents as part of the Web Payments architecture to determine which origins are authorized to distribute payment apps for a given payment method, and to discover payment app manifests associated with that payment method.[^w3c-tr]

Payment method manifests are closely associated with the [Payment Handler API](https://www.w3.org/TR/payment-handler/) and are often discussed alongside the [Payment Request API](Payment%20Request%20API.md), which is the merchant-facing API used to invoke browser-mediated payment flows.[^w3c-tr][^w3c-payment-request]

## What the manifest is for

At a high level, the payment method manifest mechanism helps a user agent answer questions such as:

- **Who is allowed to provide payment apps** for a particular payment method?
- **Where can the user agent find payment app manifests** related to that payment method?

The specification defines how the manifest is fetched and processed, and the information it can contain for these purposes.[^w3c-tr]

## Relationship to other Web Payments specs

- **Payment Request API:** lets a merchant site request a payment and receive a response. Payment method identifiers selected in Payment Request determine which payment methods are in scope for a transaction.[^w3c-payment-request]
- **Payment Handler API:** defines how web-based payment apps can register and be invoked to handle payment requests.[^w3c-payment-handler]
- **Payment Method Identifiers:** defines the identifier formats used to name payment methods in Payment Request and related flows.[^w3c-payment-method-id]

## See also

- [Payment Request API](Payment%20Request%20API.md)
- [Secure Payment Confirmation (W3C)](Secure%20Payment%20Confirmation%20(W3C).md)

## References

[^w3c-tr]: W3C. “Payment Method Manifest.” https://www.w3.org/TR/payment-method-manifest/
[^w3c-payment-handler]: W3C. “Payment Handler API.” https://www.w3.org/TR/payment-handler/
[^w3c-payment-request]: W3C. “Payment Request API.” https://www.w3.org/TR/payment-request/
[^w3c-payment-method-id]: W3C. “Payment Method Identifiers.” https://www.w3.org/TR/payment-method-id/
