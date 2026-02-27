# Indirect prompt injection

**Indirect prompt injection** is a form of *prompt injection* in which a large language model (LLM) or LLM-enabled application is influenced by **untrusted external content** (for example, a web page, document, email, or retrieved knowledge-base entry) that contains embedded instructions. When the application includes that external content in the model’s context (for example, for summarization or retrieval-augmented generation), the model may treat parts of the content as instructions and follow them, potentially causing unsafe or unintended behavior.[1][2]

Indirect prompt injection is often contrasted with **direct prompt injection** (sometimes described as "jailbreaking"), where the attacker provides the malicious instruction directly as user input.[1]

## Description

LLM-integrated applications commonly ingest external data (web browsing, file uploads, plugins, connectors, or retrieval systems). Indirect prompt injection exploits the fact that LLMs process natural-language inputs without a hard separation between *data* and *instructions*, so attacker-controlled text embedded in external content can alter the model’s behavior when it is placed into the prompt context.[2]

The OWASP GenAI Security Project describes indirect prompt injections as attacks in which an LLM accepts input from external sources that can be controlled by an attacker, allowing the attacker to "hijack" the conversation context and steer outputs or downstream actions.[1]

## Attack scenarios

Documented scenarios include:

- **Webpage summarization**: a user asks an LLM to summarize a page that contains hidden or innocuous-looking instructions; the model follows the embedded instructions instead of the user’s intent, potentially soliciting secrets or producing an attacker-chosen output.[1][2]
- **Tool / plugin misuse**: if the LLM can call tools (such as email, purchasing, or data-access plugins), injected instructions in external content can attempt to trigger unauthorized tool use.[1]

## Impacts

Reported and discussed impacts include:

- **Data exfiltration** (for example, leaking conversation history or sensitive data accessible via tools or connectors)
- **Unauthorized actions** performed via tools or downstream systems (for example, sending emails or making purchases)
- **Output manipulation** and social engineering

OWASP notes that in advanced cases a compromised LLM can effectively act as an agent for the attacker by interacting with plugins or backend systems available to the application.[1]

## Mitigations

Mitigations commonly recommended in the literature include:

- **Segregate and label untrusted content** when constructing prompts (for example, by clearly delimiting retrieved text), to reduce the chance that external data is treated as instruction.[1][2]
- **Least-privilege tool access** and strong authorization boundaries for any backend actions the LLM can request.[1]
- **Human-in-the-loop confirmation** for privileged or irreversible actions (for example, sending or deleting emails, transferring funds).[1]

Microsoft describes a defense-in-depth approach that combines **input isolation** (e.g., techniques intended to distinguish untrusted data from instructions), **detection** (e.g., prompt-injection classifiers), and **impact mitigation** via governance and consent workflows.[3]

## See also

- [Prompt injection](https://owasp.org/www-community/attacks/PromptInjection)
- [LLM01: Prompt Injection (OWASP GenAI Top 10)](https://genai.owasp.org/llmrisk2023-24/llm01-24-prompt-injection/)

## References

1. OWASP GenAI Security Project. "LLM01: Prompt Injection". https://genai.owasp.org/llmrisk2023-24/llm01-24-prompt-injection/ (accessed 2026-02-27).
2. Greshake, K.; Abdelnabi, S.; et al. "Not what you’ve signed up for: Compromising Real-World LLM-Integrated Applications with Indirect Prompt Injection". arXiv:2302.12173. https://arxiv.org/abs/2302.12173 (accessed 2026-02-27).
3. Microsoft Security Response Center (MSRC). "How Microsoft defends against indirect prompt injection attacks" (July 29, 2025). https://www.microsoft.com/en-us/msrc/blog/2025/07/how-microsoft-defends-against-indirect-prompt-injection-attacks (accessed 2026-02-27).
