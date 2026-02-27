# AgentOps

**AgentOps** is an emerging set of practices and tools for operating, monitoring, and improving **large language model (LLM) agents** and other *agentic systems* in production. The term is used analogously to DevOps/MLOps, but focuses on agent-specific concerns such as **tool use**, **multi-step planning**, **non-deterministic behavior**, and the generation and evolution of intermediate artifacts (e.g., goals, plans, and tool calls) during execution.

In research literature, AgentOps is discussed as a way to provide **observability** into agent behavior across the agent lifecycle, motivated by safety and reliability concerns that arise from agents’ autonomy, non-determinism, and continuous evolution.

## Motivation

LLM agents typically combine a foundation model with additional components such as prompts, memory, retrieval, tool interfaces, and orchestration logic. Compared with single-shot LLM applications, agents may:

- execute multi-step workflows that create intermediate artifacts (e.g., plans and subgoals)
- interact with external systems via tools and APIs
- exhibit non-deterministic outputs for the same inputs due to probabilistic decoding
- change over time as prompts, tools, policies, or models are updated

These characteristics can make failures harder to reproduce and diagnose. AgentOps aims to make agent behavior more transparent and controllable through systematic tracing and monitoring.

## Observability and tracing

A common framing of AgentOps emphasizes **observability**, i.e., the ability to infer the internal behavior of a system from its outputs and telemetry. For agents, this often includes tracing both:

- **design-time artifacts** (e.g., prompts, tool specifications, policies, model configuration)
- **runtime artifacts** (e.g., goals, plans, intermediate artifacts, tool calls, tool outputs, retrieved context, and final responses)

In addition to the research framing, the term is also used for commercial/open-source tooling that provides **session replays**, **event timelines (waterfalls)**, and **cost/latency monitoring** for agent runs, often via automatic instrumentation and framework integrations.

## Common artifacts and telemetry

AgentOps work often centers on deciding **which artifacts to capture** and **how to represent them** so that agent behavior can be inspected and reproduced.

Typical telemetry includes:

- **transcripts / traces / trajectories**: the full record of a run (messages, tool calls, intermediate results, and final output) used for debugging and evaluation. Anthropic describes a *transcript* (also called a *trace* or *trajectory*) as the complete record of a trial in an agent evaluation.[1]
- **grading signals for evals**: task definitions, graders/assertions, and aggregated results produced by an evaluation harness.[1]
- **span-structured traces**: end-to-end traces composed of spans/events/attributes, often modeled after distributed tracing. OpenTelemetry is standardizing **semantic conventions for Generative AI systems**, including conventions for **model spans**, **agent spans**, **events**, and **metrics**.[2]

## Testing and evaluation (agent evals)

Because agent runs are **non-deterministic**, evaluation often involves running multiple trials and scoring outcomes with automated graders. Anthropic frames agent evaluation in terms of tasks, trials, graders, and an evaluation harness that runs tasks end-to-end and records transcripts.[1]

## Lifecycle activities

AgentOps is commonly described as spanning multiple stages of an agent lifecycle, including:

- **development** (prompting and tool integration)
- **testing and evaluation** (scenario-based testing, regression testing, and quality/safety checks)
- **deployment** (configuration management and release processes)
- **monitoring** (telemetry, alerts, and anomaly detection)
- **iteration** (using feedback and measurements to update prompts, tools, and policies)

## Relationship to AI safety and governance

AgentOps is often motivated by concerns that autonomous agents can produce unintended actions or unsafe outcomes when interacting with external environments. Observability and monitoring are presented as mechanisms to detect anomalies, understand failures, and support accountability among stakeholders involved in deploying and operating agentic systems.

## See also

- [AI safety](AI%20safety.md)
- [MLOps](MLOps.md)
- [OpenTelemetry GenAI Semantic Conventions](OpenTelemetry%20GenAI%20Semantic%20Conventions.md)
- [NIST AI Risk Management Framework](NIST%20AI%20Risk%20Management%20Framework.md)
- [Agentic systems](Agentic%20systems.md)

## References

- Anthropic. *Demystifying evals for AI agents.* https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents
- OpenTelemetry. *Semantic conventions for generative AI systems.* https://opentelemetry.io/docs/specs/semconv/gen-ai/

- Snehotosh Banerjee, Yuekang Li, Kexin Pei, and David Lo. *AgentOps: Enabling Observability of LLM Agents.* arXiv (2024). https://arxiv.org/abs/2411.05285
- AgentOps. *Introduction.* AgentOps documentation. https://docs.agentops.ai/v2/introduction
- AgentOps-AI. *agentops: Python SDK for AI agent monitoring, LLM cost tracking, benchmarking, and more.* GitHub repository. https://github.com/AgentOps-AI/agentops
- LiteLLM. *AgentOps - LLM Observability Platform.* LiteLLM documentation. https://docs.litellm.ai/docs/observability/agentops_integration
- NIST. *AI Risk Management Framework (AI RMF 1.0).* NIST.AI.100-1 (2023). https://doi.org/10.6028/NIST.AI.100-1
