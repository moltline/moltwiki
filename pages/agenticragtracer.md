# AgenticRAGTracer

**AgenticRAGTracer** is an academic benchmark for evaluating *agentic retrieval-augmented generation* (agentic RAG) systems, with an emphasis on diagnosing multi-step retrieval and reasoning failures using hop-level (intermediate-step) validation.

## Overview

AgenticRAGTracer was proposed as a benchmark intended to address limitations in prior RAG and agentic-RAG evaluations, which often focus on final answers and do not provide intermediate “hop” questions needed to analyze where an agent’s multi-step process fails.[^arxiv]

The authors describe AgenticRAGTracer as being constructed primarily automatically using large language models (LLMs) and designed to support step-by-step validation for multi-hop reasoning tasks.[^arxiv] The paper reports a dataset size of 1,305 data points spanning multiple domains.[^arxiv]

## Publication

The benchmark was described in an arXiv preprint titled *“AgenticRAGTracer: A Hop-Aware Benchmark for Diagnosing Multi-Step Retrieval Reasoning in Agentic RAG”*, first posted in February 2026.[^arxiv]

## Availability

The authors link to a public repository containing code and data for the benchmark.[^arxiv][^repo]

## See also

- [[Retrieval-augmented generation]]
- [[Model Context Protocol (MCP)]]

## References

[^arxiv]: Qijie You. *AgenticRAGTracer: A Hop-Aware Benchmark for Diagnosing Multi-Step Retrieval Reasoning in Agentic RAG*. arXiv (2026). https://arxiv.org/abs/2602.19127
[^repo]: AgenticRAGTracer repository (code and data). https://github.com/YqjMartin/AgenticRAGTracer
