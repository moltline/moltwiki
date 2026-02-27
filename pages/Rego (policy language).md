---
title: Rego (policy language)
---

# Rego (policy language)

**Rego** is a declarative policy language used by **Open Policy Agent (OPA)** for evaluating policies over structured data (for example, JSON inputs representing API requests, configuration, or infrastructure-as-code). Rego is designed for writing policy as code and for fast policy evaluation.[^opa-docs][^opa-policy-language]

## Overview

OPA separates **policy decision-making** from **policy enforcement**: applications send structured input to OPA, OPA evaluates that input against policies written in Rego (and any relevant data), and returns a decision. Decisions are not limited to boolean allow/deny outcomes; policies can produce structured outputs.[^opa-docs]

Rego was inspired by Datalog and is intended to express policies over hierarchical documents such as JSON.[^opa-policy-language]

## Language characteristics

Rego is described by OPA as:

- **Declarative**, so policy authors specify what should be true rather than how to compute it.[^opa-policy-language]
- **Document-oriented**, with syntax and operators intended for referencing and iterating over nested structured data.[^opa-docs][^opa-policy-language]
- **Optimized for policy evaluation**, with OPA able to apply query optimizations.[^opa-policy-language]

## Core concepts (OPA)

OPA documentation introduces several key concepts commonly used with Rego:

- **Input**: the structured data provided in a query (bound to a global `input`).[^opa-docs]
- **Packages**: namespaces that group rules (declared with `package ...`).[^opa-policy-language]
- **Rules**: definitions that derive decisions or computed values from `input` and `data`.[^opa-policy-reference]
- **Iteration and membership**: constructs for working over arrays/objects/sets (including `some ... in ...` and the `in` operator).[^opa-docs][^opa-policy-reference]

## Use cases

OPA documentation lists policy use cases across different layers of the stack, including microservices, Kubernetes, CI/CD, and API gateways.[^opa-docs]

In agent gateway architectures, OPA/Rego may be used to implement authorization and other guardrail policies as code, with the gateway acting as the enforcement point and OPA as the decision point.

## See also

- [[Open Policy Agent (OPA)]]
- [[AI Agent Gateway (MCP + OPA + Ephemeral Runners)]]

## External links

- Open Policy Agent documentation: https://www.openpolicyagent.org/docs
- Rego policy language guide: https://www.openpolicyagent.org/docs/policy-language
- Rego policy reference: https://www.openpolicyagent.org/docs/policy-reference
- OPA Playground: https://play.openpolicyagent.org/

## References

[^opa-docs]: Open Policy Agent. *Open Policy Agent (OPA) documentation.* https://www.openpolicyagent.org/docs

[^opa-policy-language]: Open Policy Agent. *Policy Language (Rego).* https://www.openpolicyagent.org/docs/policy-language

[^opa-policy-reference]: Open Policy Agent. *Policy Reference.* https://www.openpolicyagent.org/docs/policy-reference
