# OpenAI Evals API

The **OpenAI Evals API** is an API surface for defining and running **evaluations (“evals”)** against model outputs. Evals are used to test whether outputs meet criteria you specify (e.g., correctness, style, safety), and are commonly used for **eval-driven development** when iterating on prompts, models, and workflows.

## What it does

From OpenAI’s guide, evals help you:

- **Describe** a task as an eval configuration.
- **Run** the eval against a dataset of test inputs.
- **Analyze results** and iterate to improve the prompt/model.

This is framed as similar to behavior-driven development (BDD): specify expected behavior, then test and iterate. 

## Core concepts

An eval configuration typically includes:

- **`data_source_config`**: how test items are structured (often a JSON Schema for items).
- **`testing_criteria`**: one or more **graders** that score/pass-fail model outputs.

When you execute an eval, you create an **eval run** that:

- references a **dataset** (commonly a JSONL file uploaded with `purpose="evals"`), and
- specifies how to generate a **sample output** per test item (e.g., using the Responses API with templated messages).

## Typical workflow (high level)

1. **Create an eval** (name + `data_source_config` + `testing_criteria`).
2. **Upload test data** (often JSONL items matching your schema).
3. **Create an eval run** referencing the eval id + file id, and a prompt template.
4. Review results in the **OpenAI dashboard** (the API response includes a `report_url`).

## Why it matters for agentic systems

In agentic applications (tool use, multi-step workflows), regressions can come from:

- prompt changes,
- model upgrades,
- tool/interface changes,
- new guardrails or policies.

An eval harness provides a repeatable **measure → improve → ship** loop, helping teams detect regressions before deployment.

## Sources

- OpenAI API guide: **Working with evals** (Evals API overview, creating evals/runs, uploading JSONL test data) — https://developers.openai.com/api/docs/guides/evals/
- OpenAI API reference: **Evals** resource — https://developers.openai.com/api/reference/resources/evals
- OpenAI developer blog: **OpenAI for Developers in 2025** (positions evals/graders as part of a production loop) — https://developers.openai.com/blog/openai-for-developers-2025/
