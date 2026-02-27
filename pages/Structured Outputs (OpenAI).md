---
title: "Structured Outputs (OpenAI)"
---

# Structured Outputs (OpenAI)

**Structured Outputs** is an OpenAI API feature for **function calling** that, when enabled, guarantees that the model-generated **function call arguments** conform to the **JSON Schema** provided in the function definition.

## Overview

OpenAI models can call developer-defined functions (tools) by emitting a function call with JSON arguments. In many applications, developers need those arguments to be reliably machine-parseable and schema-valid.

OpenAI introduced Structured Outputs as an opt-in setting on function definitions (commonly described as `strict: true`) to ensure the generated arguments match the declared JSON Schema exactly.

## Relationship to JSON mode and function calling

- **Function calling**: a mechanism for models to request that an application invoke an external tool/function, passing arguments as JSON.
- **JSON mode**: a response formatting mode intended to ensure outputs are valid JSON, but **does not** guarantee conformance to a specific schema.
- **Structured Outputs**: a stricter guarantee applied to **function call arguments**, ensuring they match the developer-provided JSON Schema.

## Use cases

Structured Outputs is commonly used for:

- **Reliable tool invocation** (e.g., passing dates, IDs, enum values, and nested objects without post-processing)
- **Data extraction pipelines** that require schema-valid JSON objects
- **Workflow automation** where downstream systems reject malformed or unexpected fields

## See also

- [Function calling | OpenAI Help Center](https://help.openai.com/en/articles/8555517-function-calling-in-the-openai-api)
- [OpenAI Responses API](/OpenAI%20Responses%20API.md)
- [OpenAI Agents SDK](/OpenAI%20Agents%20SDK.md)

## References

1. OpenAI Help Center. “Function Calling in the OpenAI API” (includes the introduction of Structured Outputs and the `strict: true` setting). https://help.openai.com/en/articles/8555517-function-calling-in-the-openai-api
