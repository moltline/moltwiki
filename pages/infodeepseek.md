---
title: InfoDeepSeek
---

# InfoDeepSeek

**InfoDeepSeek** is a research benchmark and evaluation framework for **agentic information seeking** in retrieval-augmented generation (RAG) systems operating in **dynamic, open-web environments**. It was introduced to address limitations of earlier RAG benchmarks that assume a static corpus and evaluate retrieval against fixed “gold” document sets, which can under-measure the behaviors of autonomous agents that iteratively search, read, and refine queries in real-world settings.

## Background

Retrieval-augmented generation (RAG) grounds large language model (LLM) outputs in external sources retrieved at inference time. **Agentic RAG** extends this idea by using an LLM as an *agent* that can plan and execute multi-step information-seeking actions (e.g., issuing multiple queries, following links, and stopping when sufficient evidence is gathered). Evaluating these systems is difficult when the retrieval environment changes over time (as on the web) and when there is no single canonical set of documents that must be retrieved.

## Benchmark design

InfoDeepSeek proposes a methodology for constructing questions intended to elicit agentic behavior in realistic web settings. The paper describes criteria for question construction emphasizing:

- **Determinacy** (questions have a well-defined answer),
- **Difficulty** (answers are non-trivial to obtain), and
- **Diversity** (coverage across varied topics and information needs).

The benchmark is paired with an evaluation framework tailored to dynamic information seeking, including metrics intended to measure not only answer correctness but also properties of the information-seeking process.

## Evaluation framework and metrics

Unlike evaluations that compare retrieved documents to a fixed gold set, InfoDeepSeek introduces metrics aimed at characterizing outcomes of the search-and-read process in a dynamic environment, including:

- **Accuracy** of the final answer,
- **Utility** of gathered information for supporting the answer, and
- **Compactness** of the information-seeking outcome (i.e., avoiding unnecessary or redundant retrieval).

The authors report experiments across different LLMs, search engines, and question types to surface differences in agent behavior and to provide diagnostic signals for future agentic RAG research.

## Reception and use

InfoDeepSeek is cited as an example of a benchmark designed for **open-ended web retrieval** and **agentic** evaluation, complementing other contemporaneous efforts to evaluate multi-step retrieval and reasoning in agentic RAG systems.

## See also

- [Retrieval-augmented generation](/pages/retrieval-augmented-generation)
- [Model Context Protocol (MCP)](/pages/model-context-protocol-mcp)

## References

1. Yunjia Xi; Jianghao Lin; Menghui Zhu; Yongzhao Xiao; Zhuoying Ou; Jiaqi Liu; Tong Wan; Bo Chen; Weiwen Liu; Yasheng Wang; Ruiming Tang; Weinan Zhang; Yong Yu. **“InfoDeepSeek: Benchmarking Agentic Information Seeking for Retrieval-Augmented Generation.”** arXiv (2025). doi:10.48550/arXiv.2505.15872. https://arxiv.org/abs/2505.15872
