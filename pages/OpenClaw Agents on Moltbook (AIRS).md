# OpenClaw Agents on Moltbook (AIRS)

**"OpenClaw Agents on Moltbook: Risky Instruction Sharing and Norm Enforcement in an Agent-Only Social Network"** is a 2026 research paper on arXiv that analyzes how OpenClaw agents interact on *Moltbook* (an agent-only social network), with a focus on how often agents share action-inducing instructions and whether other agents respond with norm-enforcing (safety-cautioning) replies.

## What the paper studies

The paper analyzes a Moltbook dataset of agent-generated content (posts and comments) and introduces a lexicon-based metric called the **Action-Inducing Risk Score (AIRS)** to quantify the prevalence of action-inducing language (i.e., instructions that could prompt an agent to take actions).

The authors then compare how other agents respond to posts with action-inducing language versus non-instructional posts, including whether replies attempt to discourage risky behavior.

## Reported findings (high level)

According to the paper’s abstract:

- **Action-inducing language is common**: 18.4% of posts contain action-inducing language.
- **Norm enforcement is selective**: posts containing actionable instructions are more likely to receive norm-enforcing replies that caution against unsafe or risky behavior.
- **Toxic responses are rare** across both instructional and non-instructional posts.

## Why it matters (adjacent context)

If Moltbook is used as a shared environment for many autonomous agents, then instruction sharing and social feedback can become part of the overall safety picture. This paper is relevant to Moltbook/OpenClaw discussions because it frames **social dynamics (peer responses and norm enforcement)** as an additional layer alongside technical safeguards.

## Sources

- Md Motaleb Hossen Manik. *OpenClaw Agents on Moltbook: Risky Instruction Sharing and Norm Enforcement in an Agent-Only Social Network.* arXiv (2026). https://arxiv.org/abs/2602.02625
- DOI: https://doi.org/10.48550/arXiv.2602.02625
