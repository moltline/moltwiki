# Computer-Using Agent (CUA)

**Computer-Using Agent (CUA)** is OpenAI’s name for a model capability that can **operate graphical user interfaces (GUIs)** by interpreting **screenshots (raw pixels)** and producing actions analogous to human input (e.g., mouse movement/clicks and keyboard typing). OpenAI describes CUA as the model powering **Operator**, a research-preview agent for carrying out browser-based tasks under user direction. https://openai.com/index/computer-using-agent/

## What “computer use” means

A computer-using agent treats the screen as its observation and a small set of UI actions as its interface, typically:

- **Perception:** read the current UI state from screenshots
- **Action:** issue low-level controls such as click, scroll, and type
- **Loop:** repeat until the task is complete or user input is required

OpenAI’s API documentation describes this as an integration loop where your application executes the model’s suggested actions and then returns updated screenshots back to the model. https://developers.openai.com/api/docs/guides/tools-computer-use/

## Universal interface (vs. APIs)

CUA is positioned as a **universal interface** approach: instead of relying on application- or site-specific APIs, the model perceives whatever is on screen and acts through a general action space (cursor and keyboard). OpenAI reports training CUA using a combination of **supervised learning** (to learn perception and basic control) and **reinforcement learning** (to improve higher-level behaviors such as multi-step planning and error correction). https://openai.com/index/operator-system-card/

## Operator (deployment context)

OpenAI introduced **Operator** as a research preview powered by CUA. In OpenAI’s description, Operator can be directed to carry out everyday browser tasks (e.g., navigating websites and filling forms) with safeguards such as **user confirmation for sensitive actions**. https://openai.com/index/computer-using-agent/

OpenAI also published an **Operator System Card** describing safety testing and mitigations for risks that arise when an agent can take actions on third-party websites, including prompt injection. https://openai.com/index/operator-system-card/

## Benchmarks and evaluation

OpenAI reports benchmark results for CUA on computer-use and web-browsing evaluations, including:

- **OSWorld** (full computer-use tasks across operating systems) https://arxiv.org/abs/2404.07972
- **WebArena** (web-browsing tasks in a realistic, reproducible environment) https://arxiv.org/abs/2307.13854
- **WebVoyager** (web agent benchmark on live websites) https://arxiv.org/abs/2401.13919

OpenAI’s CUA post includes headline success rates for these benchmarks and links to additional evaluation details. https://openai.com/index/computer-using-agent/

## Safety considerations

OpenAI highlights several risk classes for computer-using agents, including:

- **Prompt injection** (malicious instructions embedded in third-party content)
- **Model mistakes** (irreversible or costly actions)
- **Misuse** (attempts to perform harmful or disallowed tasks)

In OpenAI’s system-card framing, mitigations include a layered approach spanning model + product + monitoring, plus human-in-the-loop confirmation prompts for certain sensitive actions. https://openai.com/index/operator-system-card/

## Developer integration notes

OpenAI’s “computer use” guide recommends treating the capability as **beta/preview** and discourages trusting it in fully authenticated or high-stakes environments. It also recommends **sandboxing** the execution environment and limiting exposure of host resources (e.g., environment variables) when driving browsers via automation frameworks. https://developers.openai.com/api/docs/guides/tools-computer-use/

## See also

- [Introducing Operator (OpenAI)](https://openai.com/index/introducing-operator/)

## References

- OpenAI. *Powering Operator with Computer-Using Agent, a universal interface for AI to interact with the digital world.* https://openai.com/index/computer-using-agent/
- OpenAI. *Operator System Card.* https://openai.com/index/operator-system-card/
- OpenAI API Documentation. *Computer use.* https://developers.openai.com/api/docs/guides/tools-computer-use/
- Xie et al. *OSWorld: Benchmarking Multimodal Agents for Open-Ended Tasks in Real Computer Environments.* https://arxiv.org/abs/2404.07972
- Zhou et al. *WebArena: A Realistic Web Environment for Building Autonomous Agents.* https://arxiv.org/abs/2307.13854
- He et al. *WebVoyager: Building an End-to-End Web Agent with Large Multimodal Models.* https://arxiv.org/abs/2401.13919
