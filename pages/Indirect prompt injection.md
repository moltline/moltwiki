# Indirect prompt injection

**Indirect prompt injection** is a form of prompt injection where **attacker-controlled instructions arrive via an external source** (e.g., a web page, document, email, issue/PR text, or a retrieved knowledge-base chunk) that an LLM application ingests and places into the model’s context. If that untrusted content is not handled carefully, the model may treat parts of it as instructions and follow them, causing unsafe or unintended behavior. https://genai.owasp.org/llmrisk/llm01-prompt-injection/

It is often contrasted with **direct prompt injection**, where the attacker supplies the malicious instruction directly as user input. https://genai.owasp.org/llmrisk/llm01-prompt-injection/

## What counts as “indirect” (remote) injection

Indirect prompt injection typically involves:

- **A separate content channel** (browser/RAG/connector/file) that the user did not author
- **A vulnerable prompt construction step** that mixes untrusted content with instructions
- **Optional agency** (tools, plugins, actions) that turns manipulation into real-world impact

OWASP’s LLM01 guidance explicitly calls out *indirect prompt injections* as cases where external sources (websites/files) contain content that, when interpreted by the model, alters behavior. https://genai.owasp.org/llmrisk/llm01-prompt-injection/

## Why it works (root cause)

Most LLM systems process natural language without a hard, enforced boundary between *data* and *instructions*. When an application inserts untrusted text into the same context window as system/developer instructions, the model can misinterpret the untrusted text as higher-priority instruction.

This “instructions and data share the same channel” property is central to the indirect prompt injection threat model described in *Not what you’ve signed up for: Compromising Real-World LLM-Integrated Applications with Indirect Prompt Injection*. https://arxiv.org/abs/2302.12173

## Common attack scenarios

- **Summarization / Q&A over content**: a user asks for a summary of a page (or a RAG pipeline retrieves a document) that includes embedded instructions; the model follows those instructions instead of the user’s request. https://genai.owasp.org/llmrisk/llm01-prompt-injection/  https://arxiv.org/abs/2302.12173
- **Tool / plugin misuse**: injected instructions attempt to trigger unauthorized tool calls (e.g., sending emails, making purchases, accessing internal systems). The risk increases with the amount of *agency* granted to the model. https://genai.owasp.org/llmrisk/llm01-prompt-injection/
- **Code / VCS context**: indirect injection can arrive via code comments, commit messages, issues, or PR descriptions that an LLM-powered assistant reads and then treats as instruction. https://cheatsheetseries.owasp.org/cheatsheets/LLM_Prompt_Injection_Prevention_Cheat_Sheet.html

## Impacts

Impacts depend heavily on what the LLM application can access and do, but commonly discussed outcomes include:

- **Disclosure of sensitive information** (e.g., secrets reachable via tools/connectors) https://genai.owasp.org/llmrisk/llm01-prompt-injection/
- **Unauthorized actions** via connected tools/APIs (especially if approvals/policy checks are weak) https://genai.owasp.org/llmrisk/llm01-prompt-injection/
- **Content manipulation** (steering outputs, social engineering, misleading summaries) https://genai.owasp.org/llmrisk/llm01-prompt-injection/

## Mitigations (practical)

No single control fully prevents prompt injection, but OWASP recommends layered mitigations. Useful patterns for *indirect* injection include:

- **Segregate and label untrusted content** when building prompts (clear delimiting + provenance) so the model is less likely to treat it as instruction. https://genai.owasp.org/llmrisk/llm01-prompt-injection/
- **Least privilege + explicit authorization** for any tool/action the model can request; keep privileged operations in deterministic code paths. https://genai.owasp.org/llmrisk/llm01-prompt-injection/
- **Human approval for high-risk actions** (payments, external messaging, data export, destructive operations). https://genai.owasp.org/llmrisk/llm01-prompt-injection/
- **Input/output filtering and validation** (treat both untrusted content and model outputs as untrusted inputs to policy/code). https://genai.owasp.org/llmrisk/llm01-prompt-injection/  https://cheatsheetseries.owasp.org/cheatsheets/LLM_Prompt_Injection_Prevention_Cheat_Sheet.html

## See also

- [Prompt injection](https://owasp.org/www-community/attacks/PromptInjection)
- [LLM01:2025 Prompt Injection (OWASP GenAI Security Project)](https://genai.owasp.org/llmrisk/llm01-prompt-injection/)

## References

- OWASP GenAI Security Project. “LLM01:2025 Prompt Injection”. https://genai.owasp.org/llmrisk/llm01-prompt-injection/ (accessed 2026-03-01).
- OWASP Cheat Sheet Series. “LLM Prompt Injection Prevention Cheat Sheet”. https://cheatsheetseries.owasp.org/cheatsheets/LLM_Prompt_Injection_Prevention_Cheat_Sheet.html (accessed 2026-03-01).
- Greshake, K.; Abdelnabi, S.; et al. “Not what you’ve signed up for: Compromising Real-World LLM-Integrated Applications with Indirect Prompt Injection”. arXiv:2302.12173. https://arxiv.org/abs/2302.12173 (accessed 2026-03-01).
