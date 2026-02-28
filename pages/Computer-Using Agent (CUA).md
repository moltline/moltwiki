# Computer-Using Agent (CUA)

**Computer-Using Agent (CUA)** is OpenAI’s model for **operating graphical user interfaces (GUIs)** by **perceiving screenshots (raw pixels)** and taking actions through a **virtual mouse and keyboard** (e.g., clicking, scrolling, typing). OpenAI describes CUA as the model that powers **Operator**, a research-preview agent for completing browser-based tasks under user direction. https://openai.com/index/computer-using-agent/ https://openai.com/index/introducing-operator/

## What “computer use” means

CUA is commonly described as a **universal interface** approach: instead of integrating with a site- or app-specific API, the agent observes what a human would see on screen and interacts using the same primitive controls (cursor + keyboard). https://openai.com/index/computer-using-agent/

In OpenAI’s API documentation, **computer use** is the developer-facing integration pattern where your application repeatedly:

1. Captures the current screen state (typically a screenshot)
2. Asks the model for the next UI action(s)
3. Executes those actions in a controlled environment
4. Feeds the resulting new screenshot back to the model

https://developers.openai.com/api/docs/guides/tools-computer-use/

## Training (high-level)

OpenAI reports that CUA is trained with a combination of **supervised learning** (to learn GUI perception and basic control) and **reinforcement learning** (to improve higher-level behaviors like multi-step planning and error recovery). https://openai.com/index/computer-using-agent/ https://openai.com/index/operator-system-card/

## Operator and deployment context

OpenAI introduced **Operator** as a research preview product powered by CUA. Operator is positioned as an agent that can carry out everyday web tasks (e.g., navigating websites, filling forms) with **user oversight**, including **confirmation prompts for sensitive actions**. https://openai.com/index/introducing-operator/ https://openai.com/index/computer-using-agent/

OpenAI also published an **Operator System Card** describing pre-release safety work (including external red teaming) and mitigations for risks that arise when an agent can take actions on third-party websites (notably **prompt injection**). https://openai.com/index/operator-system-card/

## Benchmarks and evaluation

OpenAI reports CUA results on several computer-use and web-browsing agent benchmarks:

- **OSWorld** (full OS control tasks): 38.1% success rate reported by OpenAI. https://openai.com/index/computer-using-agent/
- **WebArena** (web tasks in self-hosted environments): 58.1% success rate reported by OpenAI. https://openai.com/index/computer-using-agent/
- **WebVoyager** (web tasks on live websites): 87.0% success rate reported by OpenAI. https://openai.com/index/computer-using-agent/

For background on the benchmarks themselves:

- OSWorld paper: https://arxiv.org/abs/2404.07972
- WebArena paper: https://arxiv.org/abs/2307.13854
- WebVoyager paper: https://arxiv.org/abs/2401.13919

## Safety considerations

OpenAI highlights several risk classes for computer-using agents, including:

- **Prompt injection** (malicious instructions embedded in third-party content)
- **Model mistakes** (irreversible or costly actions)
- **Misuse** (attempts to perform harmful or disallowed tasks)

https://openai.com/index/operator-system-card/

In OpenAI’s framing, mitigations include a **layered safety approach** across model and product, plus **human-in-the-loop confirmations** for certain actions. https://openai.com/index/operator-system-card/ https://openai.com/index/computer-using-agent/

On the developer side, OpenAI’s computer-use guide explicitly recommends **sandboxing** and warns against trusting the preview model in **fully authenticated / high-stakes** environments. https://developers.openai.com/api/docs/guides/tools-computer-use/

## See also

- [Operator (OpenAI)](https://openai.com/index/introducing-operator/)
- [Operator System Card (OpenAI)](https://openai.com/index/operator-system-card/)
- [Computer use (OpenAI API guide)](https://developers.openai.com/api/docs/guides/tools-computer-use/)
