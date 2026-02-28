# Computer-Using Agent (CUA)

A **Computer-Using Agent (CUA)** is an OpenAI model and product capability designed to **operate graphical user interfaces (GUIs)** by interpreting **screenshots (pixels)** and issuing actions analogous to human input (for example, mouse movement/clicks and keyboard typing). OpenAI describes CUA as the model that powers *Operator*, a research-preview agent that can perform web tasks under user direction.

## Overview

CUA is positioned as a *universal interface* approach: rather than relying on application- or site-specific APIs, the model perceives what is on screen and acts through a general action space (cursor and keyboard).

In OpenAI's description, CUA operates in an iterative loop:

1. The application provides the current screen state (typically a screenshot).
2. The model proposes UI actions (for example, click or type).
3. The application executes the actions in a controlled environment.
4. The updated screen state is returned to the model.

OpenAI reports training CUA with a mixture of supervised learning (for perception and basic control) and reinforcement learning (for higher-level behaviors such as multi-step planning and error correction).

## Operator and deployment context

OpenAI introduced **Operator** as a research preview agent powered by CUA. In OpenAI's description, Operator can be directed to carry out everyday browser-based tasks (for example, navigating websites and filling forms) with safeguards such as user confirmation for sensitive actions.

OpenAI also published an **Operator System Card** describing safety testing and mitigations intended to address risks arising from an agent that can take actions on the internet, including prompt injection on third-party websites.

## Benchmarks and evaluation

OpenAI reports benchmark results for CUA across computer-use and web-browsing agent evaluations, including:

- **OSWorld**, a benchmark for multimodal agents performing open-ended tasks in real computer environments across operating systems.
- **WebArena**, a realistic and reproducible web environment for evaluating language-guided agents on self-hosted websites.
- **WebVoyager**, a benchmark for end-to-end web agents that interact with live websites using multimodal inputs.

In its CUA announcement, OpenAI reports success rates of **38.1%** on OSWorld, **58.1%** on WebArena, and **87.0%** on WebVoyager.

## Safety considerations

OpenAI highlights several risk classes for computer-using agents, including:

- **Prompt injection** (malicious instructions embedded in web content)
- **Model mistakes** (irreversible or costly actions)
- **Misuse** (attempts to perform harmful or disallowed tasks)

In OpenAI's system-card framing, mitigations include layered safeguards across the model and product, as well as human-in-the-loop confirmations for certain sensitive actions.

Separately, OpenAI's API documentation for computer use emphasizes that the capability is in beta and recommends operational precautions (such as sandboxing) because preview models may be susceptible to exploits and inadvertent mistakes.

## Developer integration

OpenAI documents a *computer use* capability in its API documentation, describing an integration loop in which an application executes model-suggested UI actions and returns screenshots of the outcomes back to the model. The documentation recommends sandboxing and avoiding exposing sensitive host environment variables when integrating browser automation.

## See also

- [Operator (OpenAI)](https://openai.com/index/introducing-operator/)
- Web-browsing agent benchmarks: OSWorld, WebArena, WebVoyager

## References

1. OpenAI. *Computer-Using Agent.* https://openai.com/index/computer-using-agent/
2. OpenAI. *Operator System Card.* https://openai.com/index/operator-system-card/
3. OpenAI API Documentation. *Computer use.* https://developers.openai.com/api/docs/guides/tools-computer-use/
4. Xie, T. et al. *OSWorld: Benchmarking Multimodal Agents for Open-Ended Tasks in Real Computer Environments.* arXiv:2404.07972. https://arxiv.org/abs/2404.07972
5. Zhou, S. et al. *WebArena: A Realistic Web Environment for Building Autonomous Agents.* arXiv:2307.13854. https://arxiv.org/abs/2307.13854
6. He, H. et al. *WebVoyager: Building an End-to-End Web Agent with Large Multimodal Models.* arXiv:2401.13919. https://arxiv.org/abs/2401.13919
