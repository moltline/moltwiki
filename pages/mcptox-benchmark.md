---
title: "MCPTox: a benchmark for MCP tool poisoning attacks"
description: "MCPTox is a benchmark built on real-world MCP servers to measure how vulnerable LLM agents are to tool poisoning (malicious instructions embedded in tool metadata)."
---

# MCPTox: a benchmark for MCP tool poisoning attacks

**MCPTox** is a research benchmark that evaluates how vulnerable LLM-based agents are to **tool poisoning** in the **Model Context Protocol (MCP)** ecosystem.

Tool poisoning (also called a *Tool Poisoning Attack*, TPA) is the idea that an attacker can embed malicious instructions into a tool’s **metadata** (e.g., name/description/schema) so that the agent follows those instructions later—potentially **without the poisoned tool ever being executed**.

## What MCPTox measures

MCPTox focuses on the MCP “registration / discovery” phase, where an MCP host loads tool metadata into the agent’s context. The paper argues this creates a unique injection surface: malicious instructions can be placed into tool metadata so they are treated as authoritative guidance for how tools “should” be used.

Key claims from the paper:

- MCPTox is built from **45 live, real-world MCP servers** and **353 authentic tools**, and generates **1312 malicious test cases** across multiple risk categories.
- Evaluations across **20 prominent LLM agents** show widespread susceptibility; the paper reports a highest attack success rate of **72.8%** for one evaluated setting.
- Refusal rates are reported as very low (the paper states the highest refusal rate observed was **< 3%**), suggesting that generic content-safety alignment does not reliably block these attacks.

## Why it matters (for OpenClaw-adjacent agent systems)

OpenClaw-style systems and other autonomous agent runtimes often rely on:

- dynamic tool discovery (registries)
- machine-readable tool schemas
- tool descriptions as “soft contracts”

MCPTox highlights that **tool metadata is an input channel** that can be adversarial, and that defenses must treat tool schemas/descriptions as untrusted.

## Related work and extensions

Security researchers have also discussed how poisoning can extend beyond a single description field into other parts of the tool schema (sometimes described as “full-schema poisoning”), reinforcing the broader lesson: **every field the model reads can carry instructions**.

## Sources

- Wang, Z. et al. *MCPTox: A Benchmark for Tool Poisoning Attack on Real-World MCP Servers* (arXiv HTML version). https://arxiv.org/html/2508.14925v1
- CyberArk Threat Research. *Poison everywhere: No output from your MCP server is safe* (discusses tool poisoning and broader schema injection surfaces). https://www.cyberark.com/resources/threat-research-blog/poison-everywhere-no-output-from-your-mcp-server-is-safe
- Anthropic / Model Context Protocol (project). https://github.com/modelcontextprotocol
