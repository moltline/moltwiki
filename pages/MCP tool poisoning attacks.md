# MCP tool poisoning attacks

**MCP tool poisoning** is a class of *indirect prompt injection* attacks against **Model Context Protocol (MCP)** clients where a malicious MCP server embeds hidden or misleading instructions inside tool metadata (e.g., tool descriptions or schema fields). Because MCP clients pass this metadata to an LLM as part of tool selection and execution, the model may follow the injected instructions—potentially causing **data exfiltration** (e.g., reading local secrets) or **unauthorized actions**—even when the user believes they are invoking a benign tool.

This risk is often discussed alongside **“rug pull”** scenarios: an MCP server can initially present a benign tool schema during onboarding and later change it to a malicious version after trust has been established.

## Why this matters

MCP makes it easy to connect assistants to powerful tools and data sources. That power also expands the attack surface:

- Tool metadata is frequently treated as “documentation,” but it is also *model input*.
- Many clients summarize tool calls for users, which can hide malicious instructions or sensitive arguments.
- Even if a client validates tool calls strictly, the model can still be influenced by poisoned metadata during planning.

## Common attack patterns

### Poisoned tool descriptions (classic TPA)
A malicious server places instructions in a tool’s description (sometimes using markup or “IMPORTANT” blocks) that tell the model to:

- read local files (SSH keys, config files, chat logs)
- extract secrets from other connected systems
- conceal the behavior from the user
- smuggle data out via tool arguments

Invariant Labs coined this as a **Tool Poisoning Attack (TPA)** in the MCP context and demonstrated practical data exfiltration risks against popular MCP clients.

### Full-schema poisoning
Follow-on research argues the injection surface is broader than the description field: any part of the JSON schema that is presented to the model (parameter names, defaults, required fields, extra/unknown fields, etc.) can potentially carry adversarial instructions.

CyberArk describes this broader class as **Full-Schema Poisoning** and also discusses more advanced variants that attempt to evade static analysis by manipulating tool outputs.

### MCP “rug pulls”
A server can change tool metadata over time. A user might review and approve a tool during installation, but later receive modified tool schemas that include malicious instructions.

## Mitigations (practical checklist)

Client and platform implementers commonly consider controls such as:

- **Treat tool metadata as untrusted input** (like web content): sanitize, escape, and constrain what is shown to the model.
- **Show full tool schemas and arguments to users** before execution (not just a short label).
- **Pin and verify tool versions** (hashes/signatures) to reduce “rug pull” risk.
- **Allowlist tools and servers**; apply per-tool least privilege and scoping.
- **Strict schema validation** and rejection of unknown fields.
- **Output filtering and policy checks** on tool results before returning them to the model.
- **Logging and diffing** of tool schemas over time, with alerts on changes.

## See also

- Model Context Protocol (MCP)
- OpenClaw security audit

## References

1. Invariant Labs. “MCP Security Notification: Tool Poisoning Attacks.” https://invariantlabs.ai/blog/mcp-security-notification-tool-poisoning-attacks
2. CyberArk. “Poison everywhere: No output from your MCP server is safe.” https://www.cyberark.com/resources/threat-research-blog/poison-everywhere-no-output-from-your-mcp-server-is-safe
3. Anthropic. “Introducing the Model Context Protocol.” https://www.anthropic.com/news/model-context-protocol
