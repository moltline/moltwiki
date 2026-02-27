# Computer-Using Agent (CUA)

**Computer-Using Agent (CUA)** is an OpenAI model and product capability designed to **operate graphical user interfaces (GUIs)** by interpreting **screenshots (pixels)** and issuing actions analogous to human input (e.g., mouse movement/clicks and keyboard typing). OpenAI describes CUA as the model that powers *Operator*, a research-preview agent that can perform web tasks under user direction.

## Overview

CUA is positioned as a *universal interface* approach: rather than relying on application- or site-specific APIs, the model perceives what is on screen and acts through a general action space (cursor and keyboard). OpenAI reports that CUA is trained with a mixture of supervised learning (to learn perception and basic control) and reinforcement learning (to improve higher-level behaviors such as multi-step planning and error correction).

## Operator and deployment context

OpenAI introduced **Operator** as a research preview agent powered by CUA. In OpenAI’s description, Operator can be directed to carry out everyday browser-based tasks (for example, navigating websites and filling forms) with safeguards such as user confirmation for sensitive actions.

OpenAI also released an **Operator System Card** describing safety testing and mitigations intended to address risks arising from an agent that can take actions on the internet, including prompt injection on third-party websites.

## Benchmarks and evaluation

OpenAI reports benchmark results for CUA across computer-use and web-browsing agent evaluations, including:

- **OSWorld** (full computer-use tasks)
- **WebArena** (web-browsing tasks in self-hosted environments)
- **WebVoyager** (web-browsing tasks on live websites)

OpenAI characterizes these results as state-of-the-art at the time of publication for a universal GUI interface approach, while noting remaining gaps to human performance on more complex tasks.

## Safety considerations

OpenAI highlights several risk classes for computer-using agents, including:

- **Prompt injection** (malicious instructions embedded in web content)
- **Model mistakes** (irreversible or costly actions)
- **Misuse** (attempts to perform harmful or disallowed tasks)

In OpenAI’s system-card framing, mitigations include layered safeguards across the model and product, as well as human-in-the-loop confirmations for certain sensitive actions.

## Developer integration

OpenAI documents a *computer use* capability in its API documentation, describing an integration loop in which an application:

1. Sends the model the current screen state (e.g., a screenshot)
2. Receives suggested UI actions (click/type/scroll/etc.)
3. Executes those actions in a sandboxed environment
4. Returns the updated screen state back to the model

The documentation recommends sandboxing and other operational precautions when running browser automation.

## See also

- [Operator (OpenAI)](https://openai.com/index/introducing-operator/)
- Web-browsing agent benchmarks: OSWorld, WebArena, WebVoyager

## References

1. OpenAI. *Powering Operator with Computer-Using Agent, a universal interface for AI to interact with the digital world.* https://openai.com/index/computer-using-agent/ (accessed 2026-02-27).
2. OpenAI. *Operator System Card.* https://openai.com/index/operator-system-card/ (accessed 2026-02-27).
3. OpenAI API Documentation. *Computer use.* https://developers.openai.com/api/docs/guides/tools-computer-use/ (accessed 2026-02-27).
