---
title: Mixture-of-Depths (MoD)
---

# Mixture-of-Depths (MoD)

**Mixture-of-Depths (MoD)** is a conditional-computation approach for transformer models in which only a subset of tokens are processed at a given layer, while the remaining tokens are skipped for that layer. By selecting (routing) which token positions participate in the layer’s attention and feed-forward computations under a fixed per-layer budget, MoD aims to reduce inference compute while keeping overall model quality comparable to a fully dense transformer at similar training cost.[^santoro2024]

## Overview

Standard transformer layers apply self-attention and MLP computations to every token position in a sequence. MoD instead introduces **token-level routing across depth**:

- At each layer, the model selects up to *k* token positions to process.
- Non-selected tokens bypass the layer’s attention and MLP computations.
- The budget *k* is chosen ahead of time, yielding a static compute graph with predictable tensor sizes, while still allowing **dynamic** (input-dependent) compute allocation across tokens and layers.[^santoro2024]

## Routing mechanisms

MoD has been explored with different routing strategies, including:

- **Top-*k* routing** learned by the network to decide which tokens are processed at each layer under the fixed budget.[^santoro2024]
- **Attention-based routing** that reuses an existing attention map from a preceding layer to make routing decisions without introducing additional trainable routing parameters (an approach presented as A-MoD).[^majumdar2024]

## Motivation and claimed benefits

Proposed motivations for MoD-style routing include:

- **Compute efficiency at inference** by reducing the number of token positions that undergo expensive per-layer computations.[^santoro2024]
- **Predictable total compute** due to a fixed per-layer token budget, even though the identity of selected tokens varies by input.[^santoro2024]
- **Adaptation from pretrained models** when routing can be derived from existing model signals (e.g., attention maps) rather than adding and training separate routing components.[^majumdar2024]

## Related approaches

MoD is part of a broader family of conditional-computation techniques for transformers, which also includes methods such as mixture-of-experts (MoE) and token pruning. MoD differs in that it conditions computation on token positions across depth while constraining the number of tokens processed per layer to a fixed budget.[^santoro2024]

## References

[^santoro2024]: Adam Santoro. *Mixture-of-Depths: Dynamically allocating compute in transformer-based language models.* arXiv:2404.02258 (2024). https://doi.org/10.48550/arXiv.2404.02258

[^majumdar2024]: Souptik Kumar Majumdar. *Attention Is All You Need For Mixture-of-Depths Routing.* arXiv:2412.20875 (2024). https://doi.org/10.48550/arXiv.2412.20875
