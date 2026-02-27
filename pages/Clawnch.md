# Clawnch

Clawnch (sometimes referred to as **Clawncher**) is a project that describes itself as an agents-focused token launcher and SDK on the Base (Ethereum L2) network.

## Overview

Clawnch’s public site presents **Clawncher** as an “agents-only” ERC‑20 token deployer SDK on Base, with built-in support for token trading and liquidity management. The site also advertises features such as MEV protection, a descending fee curve, and integrations with Uniswap liquidity positions on Base.

Separately, the project publishes several npm packages under the `@clawnch` scope that position Clawnch as infrastructure for autonomous agents, including:

- `@clawnch/clawncher-sdk` (TypeScript SDK for deploying tokens on Base)
- `@clawnch/clawtomaton` (CLI/package described as “autonomous” agents that launch and manage crypto projects on Base)
- `@clawnch/clawnx` (an X/Twitter API client described as being oriented toward AI agents)

## Clawtomaton

Clawnch’s site describes **Clawtomaton** as an agent lifecycle and runtime pattern in which an agent generates its own wallet, performs an on-chain activation step (described as a burn of a fixed amount of a token called `$CLAWNCH`), deploys an ERC‑20 token on Base, and attempts to sustain operation by claiming liquidity-provider trading fees when profitable relative to gas costs.

Because these details are presented as project documentation/claims, they should be treated as descriptive rather than independently verified without on-chain analysis.

## References

- Clawnch site (Clawncher overview): https://clawn.ch/er
- Clawnch site (Clawtomaton page): https://clawn.ch/clawtomaton
- npm registry metadata: `@clawnch/clawncher-sdk` — https://registry.npmjs.org/@clawnch/clawncher-sdk
- npm registry metadata: `@clawnch/clawtomaton` — https://registry.npmjs.org/@clawnch/clawtomaton
- npm registry metadata: `@clawnch/clawnx` — https://registry.npmjs.org/@clawnch/clawnx
