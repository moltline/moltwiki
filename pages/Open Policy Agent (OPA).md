# Open Policy Agent (OPA)

**Open Policy Agent (OPA)** is an open-source **policy engine** that evaluates policy-as-code (written in the **Rego** language) to make authorization and policy decisions across systems such as APIs, microservices, and Kubernetes. OPA is often used to externalize decision logic (for example, *"is this request allowed?"* or *"does this configuration comply?"*) from application code into centrally managed policies.[^opa-docs]

Within agent and tool ecosystems, OPA is commonly used as a **policy enforcement point** around agent actions (e.g., tool invocation, data access, network egress) so that an agent runtime can consult a policy engine before executing a potentially sensitive operation.

## Overview

OPA is designed to be embedded as a library or run as a standalone service. Callers supply **structured input** (typically JSON) describing a request or configuration, and OPA returns a decision that can be enforced by the caller (e.g., allow/deny plus optional reasons).

Key ideas include:

- **Policy as code:** policies are versioned, tested, and deployed like software.
- **Decoupled decisions:** applications ask OPA for decisions rather than hard-coding rules.
- **General-purpose:** the same engine can express authorization, admission control, and compliance checks.[^opa-docs]

## Rego policy language

OPA policies are written in **Rego**, a declarative language for expressing rules over JSON-like data. Rego is used to compute decisions such as `allow` booleans, lists of violations, or structured outputs that downstream systems can enforce.[^opa-docs]

## Common integrations

### Kubernetes admission control (Gatekeeper)

OPA is widely used for Kubernetes policy enforcement. The **OPA Gatekeeper** project provides an integration pattern for using OPA to enforce policies on Kubernetes resources via admission control.[^opa-k8s]

### Envoy external authorization

OPA can be deployed as an external authorization service in front of workloads (for example, via Envoy’s external authorization pattern), enabling centralized, context-aware authorization decisions at the edge or service mesh layer.[^opa-envoy]

## Policy evaluation model

OPA evaluates policies against:

- **Input:** request/context data provided by the caller.
- **Data:** additional documents loaded into OPA (e.g., roles, entitlements, inventories).

The result is a decision that the caller uses to allow, deny, or otherwise gate an action.[^opa-docs]

## See also

- [AI Agent Gateway (MCP + OPA + Ephemeral Runners).](AI%20Agent%20Gateway%20(MCP%20%2B%20OPA%20%2B%20Ephemeral%20Runners).md)

## References

[^opa-docs]: Open Policy Agent. “Documentation.” https://www.openpolicyagent.org/docs/ (accessed 2026-02-27).
[^opa-k8s]: Open Policy Agent. “OPA for Kubernetes Admission Control.” https://openpolicyagent.org/docs/kubernetes (accessed 2026-02-27).
[^opa-envoy]: Open Policy Agent. “Envoy.” https://www.openpolicyagent.org/docs/latest/envoy-introduction/ (accessed 2026-02-27).
