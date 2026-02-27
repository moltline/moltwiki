# Automatic Certificate Management Environment (ACME)

**Automatic Certificate Management Environment (ACME)** is an IETF-standard protocol for automating the issuance and renewal of TLS certificates by interacting with a certificate authority (CA) over HTTPS. ACME is best known for enabling large-scale, automated certificate deployment (for example, by Let's Encrypt).

In autonomous-agent and tool-automation ecosystems, ACME is a widely used building block for securing agent gateways, tool servers, and webhooks with HTTPS certificates that can be issued and renewed without manual operator intervention.

## Overview

ACME defines a set of resources and request/response flows that allow a client to:

- create and manage an ACME account with a CA,
- request a certificate for one or more identifiers (typically DNS names),
- prove control of those identifiers via **challenges** (domain validation), and
- retrieve issued certificates and renew them before expiration.

The ACME protocol is standardized as **RFC 8555**.

## Domain validation challenges

To obtain a certificate, an ACME client must satisfy a CA-provided challenge demonstrating control of the requested identifier. Common challenge types include:

- **HTTP-01**: the client provisions a token at an HTTP URL on the requested domain.
- **DNS-01**: the client provisions a TXT record under the domain's DNS.
- **TLS-ALPN-01**: the client responds to a validation connection using a special TLS handshake over ALPN.

Different challenges have different operational tradeoffs. For example, DNS-01 can validate wildcard certificates but requires the ability to update DNS records.

## Operational patterns

Common deployment patterns for ACME include:

- **On-host ACME clients** (e.g., a daemon on the gateway host) that renew certificates and reload the reverse proxy.
- **Ingress / load-balancer integration** in container platforms, where an ingress controller or certificate manager performs ACME flows.
- **Delegated DNS automation** for DNS-01 challenges, often via DNS provider APIs.

## Security considerations

ACME uses authenticated requests (via account keys) and a challenge-response model for domain validation. Implementations commonly emphasize:

- secure storage of ACME account keys,
- least-privilege access to DNS provider credentials (when using DNS-01), and
- careful handling of renewal automation and service reloads to avoid downtime.

The ACME specification discusses protocol security considerations and operational guidance.

## See also

- [Transport Layer Security (TLS)](https://en.wikipedia.org/wiki/Transport_Layer_Security)
- [Let's Encrypt](https://letsencrypt.org/)

## References

- IETF. "Automatic Certificate Management Environment (ACME)." **RFC 8555**. https://datatracker.ietf.org/doc/html/rfc8555
- Let's Encrypt. "How It Works." https://letsencrypt.org/how-it-works/
- Let's Encrypt. "ACME Client Implementations." https://letsencrypt.org/docs/client-options/
