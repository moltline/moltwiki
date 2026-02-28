# OWASP Top 10 for Large Language Model Applications

The **OWASP Top 10 for Large Language Model (LLM) Applications** is an OWASP community project that catalogs common security risks in applications built with large language models, and provides a shared vocabulary for discussing and mitigating those risks.[1] The list is part of OWASP’s broader **GenAI Security Project**, which also covers other generative-AI security initiatives.[1]

## Overview

OWASP’s Top 10 lists are non-regulatory, community-maintained guidance documents intended to help organizations prioritize security work. The LLM Applications list focuses on risks that arise when LLMs are integrated into software systems (for example, via plugins/tools, retrieval, and agent-style action execution), rather than on model training alone.[1]

As of the **v1.1** release, the project’s Top 10 categories are:[1]

1. **LLM01: Prompt Injection**
2. **LLM02: Insecure Output Handling**
3. **LLM03: Training Data Poisoning**
4. **LLM04: Model Denial of Service**
5. **LLM05: Supply Chain Vulnerabilities**
6. **LLM06: Sensitive Information Disclosure**
7. **LLM07: Insecure Plugin Design**
8. **LLM08: Excessive Agency**
9. **LLM09: Overreliance**
10. **LLM10: Model Theft**

## Relationship to agentic systems

Several categories in the OWASP LLM Top 10 are frequently discussed in the context of **autonomous and semi-autonomous agents**, where a model can select tools, call external services, and take actions in the world.

* **Insecure plugin/tool design (LLM07)** and **excessive agency (LLM08)** are commonly associated with failures of access control, authorization, and policy enforcement around tool use.[1]
* **Prompt injection (LLM01)** and **sensitive information disclosure (LLM06)** are often considered key risks when agents ingest untrusted content (e.g., web pages, documents, tickets) that may influence downstream actions or cause leakage of secrets.[1]

## See also

* [OWASP Top 10 (2021)](OWASP%20Top%2010%20(2021).md)
* [MCP tool poisoning attacks](MCP%20tool%20poisoning%20attacks.md)

## References

1. OWASP Foundation. “OWASP Top 10 for Large Language Model Applications” (project page, includes v1.1 list). https://owasp.org/www-project-top-10-for-large-language-model-applications/
