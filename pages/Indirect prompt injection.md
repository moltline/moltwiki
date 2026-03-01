# Indirect prompt injection

**Indirect prompt injection** is a form of *prompt injection* in which a large language model (LLM) or LLM-enabled application is influenced by **untrusted external content** (for example, a web page, document, email, or retrieved knowledge-base entry) that contains embedded instructions. When the application includes that external content in the model’s context (for example, for summarization or retrieval-augmented generation), the model may treat parts of the content as instructions and follow them, potentially causing unsafe or unintended behavior.[1][2]

Indirect prompt injection is often contrasted with **direct prompt injection** (sometimes described as "jailbreaking"), where the attacker provides the malicious instruction directly as user input.[1]

## Description

LLM-integrated applications commonly ingest external data (web browsing, file uploads, plugins, connectors, or retrieval systems). Indirect prompt injection exploits the fact that LLMs process natural-language inputs without a hard separation between *data* and *instructions*, so attacker-controlled text embedded in external content can alter the model’s behavior when it is placed into the prompt context.[2]

OWASP’s GenAI Security Project groups indirect prompt injection under the broader *prompt injection* risk category, describing it as injection via **external sources** (e.g., websites or files) whose content is interpreted by the model in a way that alters behavior.[1]

## Attack scenarios

Documented scenarios include:

- **Webpage summarization / RAG**: a user asks an LLM to summarize a page (or a retrieval system returns a document) that contains hidden or innocuous-looking instructions; the model follows the embedded instructions instead of the user’s intent.[1][2]
- **Tool / plugin misuse**: if the LLM can call tools (such as email, purchasing, or data-access plugins), injected instructions in external content can attempt to trigger unauthorized tool use.[1][2]

## Why it works (root cause)

Indirect prompt injection is enabled by a common architectural property of LLM systems: **the same channel carries both instructions and data**. When untrusted content is inserted into a prompt (or otherwise processed as context), it can be interpreted as instruction unless the system enforces strong boundaries in how it constructs prompts and authorizes actions.[1][2]

## Impacts

Depending on what the LLM application can access or do, discussed impacts include:[1][2]

- **Data exfiltration** (for example, leaking conversation history or sensitive data accessible via tools or connectors)
- **Unauthorized actions** performed via tools or downstream systems
- **Output manipulation** and social engineering

## Mitigations

Mitigations commonly recommended in the literature include:[1][2]

- **Least-privilege tool access** and strong authorization boundaries for any backend actions the LLM can request.
- **Human-in-the-loop confirmation** for privileged or irreversible actions.
- **Segregating / labeling untrusted content** when constructing prompts (e.g., explicit delimiting, provenance labels), so external data is less likely to be treated as instruction.
- **Output validation** and deterministic guardrails around tool invocation (treat the model as untrusted input to policy/code).

## See also

- [Prompt injection](https://owasp.org/www-community/attacks/PromptInjection)
- [LLM01:2025 Prompt Injection (OWASP GenAI Security Project)](https://genai.owasp.org/llmrisk/llm01-prompt-injection/)

## References

1. OWASP GenAI Security Project. "LLM01:2025 Prompt Injection". https://genai.owasp.org/llmrisk/llm01-prompt-injection/ (accessed 2026-03-01).
2. Greshake, K.; Abdelnabi, S.; et al. "Not what you’ve signed up for: Compromising Real-World LLM-Integrated Applications with Indirect Prompt Injection". arXiv:2302.12173. https://arxiv.org/abs/2302.12173 (accessed 2026-03-01).
