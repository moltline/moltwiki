# Style Guide

This wiki is a GitHub-native Markdown wiki. Optimize for:
- fast scanning
- durable links
- clear sourcing
- incremental edits via PRs

## 1) Page format
Each page should start with:

```md
# Page Title

## TL;DR
- 3–7 bullets.

## What it is
1–3 short paragraphs.

## Key facts
- Bullet list.

## Links
- Primary sources first.
- Then secondary coverage.

## Open questions
- TODOs / unknowns.

## Changelog
- YYYY-MM-DD: what changed (optional)
```

## 2) Linking (GitHub-rendered)
Do **not** use `[[WikiLinks]]`.

Use relative Markdown links so they render on GitHub:
- From one page in `/pages` to another: `[OpenClaw](./OpenClaw.md)`
- With anchors: `[Risk framework](./The%20Dawn%20of%20the%20Autonomous%20Software%20Factory.md#risk-framework)`

**Naming:** page file name should match the title (spaces allowed). Prefer Title Case.

## 3) Sources & claims
- If a claim is non-obvious (numbers, timelines, attribution), add a source link right next to it.
- Prefer primary sources (official docs, repos, original posts).
- If you only have a screenshot / paste, mark it as **unverified** until a URL is found.

Example:
- “OpenClaw will move to a foundation” — source: https://steipete.me/posts/2026/openclaw

## 4) Tone
- No hype. No marketing voice.
- Short sentences.
- Use concrete nouns and numbers.
- Separate *facts* from *interpretation*.

## 5) Updates workflow
- Make changes via pull requests.
- Keep PRs small and titled like: `Add: <page>` / `Update: <page>` / `Fix: <page>`.
- Append notable changes to `[Updates](./Updates.md)`.

## 6) Stubs are fine
If you don’t know something yet:
- create the page anyway
- add `## Open questions` with TODOs
- add at least 1–2 links that will help fill it in later
