---
title: Open Agentic Schema Framework (OASF)
description: A schema framework for describing AI agent records, capabilities, and taxonomies.
---

# Open Agentic Schema Framework (OASF)

The **Open Agentic Schema Framework (OASF)** is an open schema framework for describing *agentic AI* records (metadata about AI agents), including their capabilities and related taxonomies. It is intended to support interoperability and discovery across agent ecosystems by providing a standardized, attribute-based schema and supporting tooling (for example, schema validation and a schema server for browsing versions and taxonomies).

OASF is published as an open-source project and is described by its maintainers as being inspired by the **Open Cybersecurity Schema Framework (OCSF)** data modeling approach.

## Overview

OASF defines a set of schema objects and conventions for representing information about agents and their capabilities.

According to the project documentation, OASF aims to:

- Provide common data structures for representation and interoperability.
- Support unique identification and discovery of agents.
- Enable extension via additional schema modules and private extensions.

## Key concepts

### Record object

Project documentation describes a **record object** as a primary data structure for representing collections of information and metadata relevant to agentic AI applications.

### Skills, domains, and modules

OASF records can be annotated using:

- **Skills** and **domains**: taxonomies intended to support announcement and discovery across agentic systems.
- **Modules**: a mechanism for extending records with additional information in a modular way.

## Schema server

OASF maintainers provide a hosted schema server intended for browsing the schema and related taxonomies (for example, skill categories).

## Versioning and immutability

The project documentation describes a versioning policy where released schema versions are intended to be immutable, with subsequent structural changes occurring in later versions (with limited exceptions for non-breaking fixes such as documentation updates or minor corrections).

## References

- Open Agentic Schema Framework (OASF) repository. GitHub: agntcy/oasf. https://github.com/agntcy/oasf
- OASF hosted schema server. https://schema.oasf.outshift.com/
- Open Cybersecurity Schema Framework (OCSF). https://ocsf.io/
