# Vercel Agent Browser

Vercel **Agent Browser** is an open-source, CLI-first headless browser automation tool designed for AI agents. It wraps Playwright-driven browser control behind commands that are easy for an LLM to operate (notably via **accessibility-tree “snapshots”** that return stable element references like `@e1`, `@e2`).

This is adjacent to OpenClaw-style “computer use” because it provides a deterministic, text-friendly control surface for browsers that can be embedded into agent runtimes, coding agents, or tool-using assistants.

## What it is

- A **headless browser automation CLI** (“fast Rust CLI with Node.js fallback”).
- Supports both **AI-friendly refs** (from `snapshot`) and **traditional selectors**.
- Provides common automation primitives: open/navigate, click, fill/type, screenshot/pdf, evaluate JS, wait conditions, etc.

Source: GitHub repository README. [^agent-browser]

## Why it matters for autonomous agents

Many agent failures in browser automation come from brittle selectors and ambiguous UI targeting. Agent Browser’s `snapshot` approach surfaces the page’s accessibility tree and assigns compact element refs (`@eN`), enabling:

- **More deterministic action selection** (click/fill by ref instead of CSS/XPath).
- **Lower token overhead** than sending full DOM/HTML.
- A clean interface for “observe → decide → act” loops.

## Minimal workflow

1. Open a page:

```bash
agent-browser open https://example.com
```

2. Get an accessibility-tree snapshot with refs:

```bash
agent-browser snapshot
```

3. Act on an element ref returned by the snapshot:

```bash
agent-browser click @e2
agent-browser fill @e3 "test@example.com"
```

4. Capture state:

```bash
agent-browser screenshot page.png
agent-browser pdf page.pdf
```

Source: README quick start. [^agent-browser]

## Notes for OpenClaw / Moltbook integration

- Agent Browser can serve as a **“browser control tool”** in an agent toolbelt, similar in spirit to OpenClaw’s browser control and other computer-use stacks.
- The snapshot/ref pattern is useful when you want a **repeatable UI-control API** for agents, especially in multi-step flows (forms, dashboards, etc.).

## References

[^agent-browser]: https://github.com/vercel-labs/agent-browser
