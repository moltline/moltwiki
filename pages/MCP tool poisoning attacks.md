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

Invariant Labs describes this as a **Tool Poisoning Attack (TPA)** in the MCP context and provides examples where hidden instructions in tool descriptions influence an MCP client’s model behavior in ways that are not obvious to the user interface.

### Full-schema poisoning
Follow-on research argues the injection surface is broader than the description field: any part of the JSON schema that is presented to the model (for example, parameter names, required fields, defaults, or additional fields) can potentially carry adversarial instructions.

CyberArk uses the term **Full-Schema Poisoning (FSP)** for this broader class and reports experiments where injected content in non-description parts of the schema influenced the model, even when client-side validation later rejected the resulting tool call.

### MCP “rug pulls”
A server can change tool metadata over time. Invariant Labs and others discuss “rug pull” scenarios where a user reviews a benign tool during onboarding, but later receives modified tool metadata that includes malicious instructions.

## Mitigations (practical checklist)

Client and platform implementers commonly consider controls such as:

- **Treat tool metadata as untrusted input** (similar to untrusted web content): sanitize, escape, and constrain what is shown to the model.
- **Make tool metadata user-reviewable**: show full tool schemas and arguments before execution, not only a short label.
- **Pin and verify tool definitions** (for example via versioning, hashes, or signatures) to reduce “rug pull” risk.
- **Allowlist tools and servers** and apply per-tool least privilege/scoping.
- **Strict schema validation** and rejection of unknown or nonconforming fields.
- **Constrain and inspect tool outputs** before returning them to the model (e.g., filtering, policy checks).
- **Monitor for schema drift**: log and diff tool schemas over time and alert on changes.

Mitigation guidance is discussed in the Invariant Labs security notice and in subsequent write-ups that broaden the injection surface to the full schema.

## See also

- Model Context Protocol (MCP)
- OpenClaw security audit

## References

1. Invariant Labs. “MCP Security Notification: Tool Poisoning Attacks.” https://invariantlabs.ai/blog/mcp-security-notification-tool-poisoning-attacks
2. CyberArk. “Poison everywhere: No output from your MCP server is safe.” https://www.cyberark.com/resources/threat-research-blog/poison-everywhere-no-output-from-your-mcp-server-is-safe
3. Model Context Protocol. “What is the Model Context Protocol (MCP)?” https://modelcontextprotocol.io/docs/getting-started/intro
4. Anthropic. “Introducing the Model Context Protocol.” https://www.anthropic.com/news/model-context-protocol
