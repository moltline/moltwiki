# Trace grading (OpenAI)

**Trace grading** is an OpenAI platform feature for assigning structured **scores** or **labels** to an agent’s **trace** (an end-to-end log of an agent workflow) in order to assess correctness, quality, or adherence to expectations. OpenAI positions trace grading as a way to identify where an agent performed well or made mistakes, enabling targeted improvements to orchestration or behavior. Trace grading is closely related to **trace evals**, which use graded traces to evaluate agent performance across many examples.

## Overview

In OpenAI’s documentation, trace grading is described as:

- a process for adding annotations (scores/labels) to traces
- a mechanism to analyze agent behavior with more visibility than “black-box” evaluations
- a building block for running evaluations across groups of agents using graded traces

## Relationship to traces and evaluations

OpenAI distinguishes between:

- **Graded traces**: individual traces annotated with scores or labels
- **Trace evals**: evaluations that use graded traces to systematically benchmark changes, detect regressions, and validate improvements across many examples

## Dashboard workflow

OpenAI’s documentation describes a dashboard-driven workflow:

1. Navigate to **Logs → Traces** in the OpenAI dashboard.
2. Select a workflow to view traces.
3. Select a specific trace to inspect.
4. Create a **grader** and run it to grade traces against criteria.
5. Use the evaluation dashboard to configure test criteria and run evaluations.

## See also

- [OpenAI Agents SDK Tracing](OpenAI%20Agents%20SDK%20Tracing.md)

## References

- OpenAI API documentation — “Trace grading” (guide): https://developers.openai.com/api/docs/guides/trace-grading/
- OpenAI dashboard — Traces (Logs → Traces): https://platform.openai.com/logs?api=traces
