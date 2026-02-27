---
title: Open Agentic Schema Framework (OASF)
description: A schema system for describing AI agent metadata and capabilities, developed by AGNTCY/Outshift.
---

# Open Agentic Schema Framework (OASF)

The **Open Agentic Schema Framework (OASF)** is an open, standardized schema system for describing AI agent metadata, capabilities, and related taxonomies, intended to support interoperability and discovery across agentic systems.[^oasf-repo] The project is developed under the **AGNTCY** organization (an initiative associated with **Outshift by Cisco**).[^oasf-repo][^oasf-schema-site]

## Overview

OASF provides a structured way to represent information about agentic systems using versioned schemas and attribute-based taxonomies.[^oasf-repo] The project describes itself as being inspired by the **Open Cybersecurity Schema Framework (OCSF)** in its data-modeling approach and implementation patterns.[^oasf-repo]

OASF includes:

- **Schema definitions** (including an extensible “record” object) for describing agent-related data.[^oasf-repo]
- **Taxonomies** for categorizing skills and domains to support announcement and discovery.[^oasf-repo][^oasf-schema-site]
- A **schema server** for browsing and validating the schema.[^oasf-repo]

## Schema server

OASF is published with a web-accessible schema server that can be used to browse schema content and, in some configurations, validate records.[^oasf-repo][^oasf-schema-site]

## Relationship to MCP tooling

The OASF repository documents an MCP (Model Context Protocol) server within the AGNTCY ecosystem intended to assist in creating and validating OASF records when used with an LLM-enabled client (for example, an MCP-compatible IDE).[^oasf-repo]

## See also

- [[Agent Directory Service (AGNTCY ADS)]]
- [[Model Context Protocol (MCP)]]

## References

[^oasf-repo]: AGNTCY. “Open Agentic Schema Framework (OASF)” (GitHub repository). https://github.com/agntcy/oasf

[^oasf-schema-site]: Outshift by Cisco / AGNTCY. “Open Agentic Schema Framework” (schema site). https://schema.oasf.outshift.com/
