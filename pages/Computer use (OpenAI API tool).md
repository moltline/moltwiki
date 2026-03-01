# Computer use (OpenAI API tool)

**Computer use** is a tool capability in the **OpenAI Responses API** that enables a model to propose **graphical user interface (GUI)** actions (for example, clicking at coordinates or typing text) while an external program executes those actions in a **browser or virtual machine** and returns **screenshots** (or other state) back to the model in a loop.[^openai-computer-use-guide]

Computer use is closely associated with OpenAI’s **Computer-Using Agent (CUA)** model family (for example, `computer-use-preview`), which is described as combining vision and reasoning to operate computer interfaces.[^openai-cua-post]

## Overview

In OpenAI’s documentation, computer use is implemented as an *interaction loop*:

1. A developer sends a request to the model that includes the computer-use tool configuration (for example, display size and environment).
2. The model returns one or more **computer actions** (such as a click or a request for a screenshot).
3. The developer’s program executes the action in the target environment (for example, a controlled browser session).
4. The program captures the updated state (commonly a screenshot) and sends it back to the model, continuing until completion.[^openai-computer-use-guide]

OpenAI positions this approach as a way to automate tasks that are difficult to accomplish through site-specific APIs alone, such as multi-step workflows that require interacting with standard web UI elements.[^openai-computer-use-guide]

## Environments

OpenAI documentation and examples describe using computer use with environments such as:

- A **browser automation** environment (for example, using Playwright or Selenium to drive a browser and provide screenshots).[^openai-computer-use-guide]
- A **local or containerized virtual machine** environment where the program can execute UI actions and capture the screen.[^openai-computer-use-guide]

Microsoft’s Azure OpenAI documentation describes a similar loop for Computer Use in Azure OpenAI (classic), including tool configuration (display size and environment) and returning screenshots as tool outputs, and notes that access may be limited and region-dependent.[^azure-computer-use]

## Safety and operational guidance

OpenAI’s guide describes computer use as a preview/beta capability and recommends operational precautions, including **sandboxing** and avoiding fully authenticated or high-stakes environments while the model is in preview.[^openai-computer-use-guide]

Microsoft’s documentation describes safety checks for computer-use calls, including checks intended to help mitigate prompt injection and warnings for sensitive domains (based on the current URL when provided).[^azure-computer-use]

## Relationship to OpenClaw-style automation

In OpenClaw-adjacent systems, “computer use” is often used as a generic term for agents that can operate GUIs using screenshots and action outputs. OpenAI’s computer-use tool is one concrete implementation of this pattern via the Responses API, where the model emits structured actions and an external runner executes them and returns updated visual state.[^openai-computer-use-guide]

## See also

- [Computer-Using Agent (CUA)](Computer-Using%20Agent%20(CUA).md)
- [OpenAI Responses API](OpenAI%20Responses%20API.md)

## References

[^openai-computer-use-guide]: OpenAI. *Computer use | OpenAI API.* https://developers.openai.com/api/docs/guides/tools-computer-use/ (accessed 2026-02-28).

[^openai-cua-post]: OpenAI. *Powering Operator with Computer-Using Agent, a universal interface for AI to interact with the digital world.* https://openai.com/index/computer-using-agent/ (accessed 2026-02-28).

[^azure-computer-use]: Microsoft Learn. *Computer Use (preview) in Azure OpenAI (classic).* https://learn.microsoft.com/en-us/azure/foundry-classic/openai/how-to/computer-use (accessed 2026-02-28).
