# Agentgateway

**Agentgateway** is an open-source, AI-native proxy (gateway) intended to provide connectivity, security, and observability for agentic systems, including agent-to-agent and agent-to-tool interactions. The project originated at Solo.io and was accepted as a Linux Foundation project in 2025.

## Overview

Agentgateway positions itself as a purpose-built “data plane” for agentic workloads, aiming to govern and secure communication across interactions such as agent-to-agent, agent-to-tool, and agent-to-LLM provider APIs. The project advertises support for emerging interoperability protocols including Agent2Agent (A2A) and Anthropic’s Model Context Protocol (MCP).<ref name="lf-prnewswire" />

## History

In August 2025, the Linux Foundation announced that it welcomed the agentgateway project into its portfolio of open source initiatives, describing it as an open-source, AI-native proxy created by Solo.io for agentic AI environments.<ref name="lf-prnewswire" />

## Features

Public project materials describe the following capabilities:

* **Security and governance** features such as role-based access control (RBAC) targeted at MCP/A2A use cases.<ref name="agentgateway-github" />
* **Observability** integration via OpenTelemetry (as described by the Linux Foundation announcement).<ref name="lf-prnewswire" />
* **Dynamic configuration** updates (for example, via xDS) and multi-tenant support.<ref name="agentgateway-github" />
* **Protocol support** including A2A and MCP.<ref name="lf-prnewswire" /><ref name="agentgateway-github" />

## Relationship to the agent ecosystem

Agent gateways are sometimes described as an infrastructure layer that can enforce policy, authentication/authorization, and telemetry for interactions between agents and external tools. In coverage of the MCP ecosystem, Agentgateway has been discussed alongside MCP server discovery efforts (such as the MCP Registry) as part of a broader push toward standardized, governable agentic tooling.<ref name="infoq" />

## References

<references>
<ref name="lf-prnewswire">Linux Foundation. "Linux Foundation Welcomes Agentgateway Project to Accelerate AI Agent Adoption While Maintaining Security, Observability and Governance" (press release via PR Newswire), 25 August 2025. https://www.prnewswire.com/news-releases/linux-foundation-welcomes-agentgateway-project-to-accelerate-ai-agent-adoption-while-maintaining-security-observability-and-governance-302534106.html</ref>
<ref name="agentgateway-github">agentgateway/agentgateway. "Next Generation Agentic Proxy for AI Agents and MCP servers" (GitHub repository). https://github.com/agentgateway/agentgateway</ref>
<ref name="infoq">Hoblitzell, Andrew. "Introducing the MCP Registry" (InfoQ), 2025. https://www.infoq.com/news/2025/09/introducing-mcp-registry/</ref>
</references>
