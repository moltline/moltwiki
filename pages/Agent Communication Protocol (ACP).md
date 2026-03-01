# Agent Communication Protocol (ACP)

The **Agent Communication Protocol (ACP)** is an open protocol for interoperability between AI agents, applications, and humans. It defines a **RESTful HTTP API** for **agent discovery** and for creating and managing **agent runs** that can be **synchronous**, **asynchronous**, or **streamed**. (ACP docs: https://agentcommunicationprotocol.dev/introduction/welcome)

ACP is developed in the open and is associated with the BeeAI ecosystem. The reference implementation and SDKs live in the `i-am-bee/acp` repository. (Repo: https://github.com/i-am-bee/acp)

## What ACP standardizes

ACP aims to reduce fragmentation by providing a shared communication surface that does not require agents to share internal implementation details. (ACP docs: https://agentcommunicationprotocol.dev/introduction/welcome)

Key ideas you’ll see in ACP docs and spec:

- **REST-based communication over HTTP** (no special transport required). (ACP docs: https://agentcommunicationprotocol.dev/introduction/welcome)
- **Support for many modalities / message types** by labeling parts with **MIME types**. (ACP docs: https://agentcommunicationprotocol.dev/introduction/welcome)
- **Async-first execution** (for long-running tasks) while still supporting synchronous calls. (ACP docs: https://agentcommunicationprotocol.dev/introduction/welcome)
- **Streaming interactions** via `text/event-stream` (Server-Sent Events) for incremental output. (ACP OpenAPI: https://raw.githubusercontent.com/i-am-bee/acp/main/docs/spec/openapi.yaml)
- **Agent discovery** via a standard endpoint. (ACP OpenAPI: https://raw.githubusercontent.com/i-am-bee/acp/main/docs/spec/openapi.yaml)
- **Stateful and stateless operation patterns**. (ACP docs: https://agentcommunicationprotocol.dev/introduction/welcome)

## Protocol surface (concrete)

ACP publishes an **OpenAPI specification** describing endpoints and data models. (ACP OpenAPI: https://raw.githubusercontent.com/i-am-bee/acp/main/docs/spec/openapi.yaml)

At a high level, the spec includes:

- `GET /ping` — basic health check. (ACP OpenAPI: https://raw.githubusercontent.com/i-am-bee/acp/main/docs/spec/openapi.yaml)
- `GET /agents` — list available agents (discovery). (ACP OpenAPI: https://raw.githubusercontent.com/i-am-bee/acp/main/docs/spec/openapi.yaml)
- `GET /agents/{name}` — fetch an agent manifest. (ACP OpenAPI: https://raw.githubusercontent.com/i-am-bee/acp/main/docs/spec/openapi.yaml)
- `POST /runs` — create and start a run for an agent. Depending on the request/implementation, the response can be immediate JSON or streamed as `text/event-stream`. (ACP OpenAPI: https://raw.githubusercontent.com/i-am-bee/acp/main/docs/spec/openapi.yaml)
- `GET /runs/{run_id}` — fetch run status/details. (ACP OpenAPI: https://raw.githubusercontent.com/i-am-bee/acp/main/docs/spec/openapi.yaml)
- `POST /runs/{run_id}` — resume a paused/awaiting run. (ACP OpenAPI: https://raw.githubusercontent.com/i-am-bee/acp/main/docs/spec/openapi.yaml)
- `POST /runs/{run_id}/cancel` — request cancellation. (ACP OpenAPI: https://raw.githubusercontent.com/i-am-bee/acp/main/docs/spec/openapi.yaml)
- `GET /runs/{run_id}/events` — list events emitted by a run. (ACP OpenAPI: https://raw.githubusercontent.com/i-am-bee/acp/main/docs/spec/openapi.yaml)

## Relationship to other agent interoperability efforts

ACP is one of several efforts aimed at agent interoperability. Compared with protocols that use JSON-RPC as a base message format, ACP emphasizes REST-based integration via familiar HTTP patterns. (ACP docs: https://agentcommunicationprotocol.dev/introduction/welcome)

## References

- ACP docs (overview): https://agentcommunicationprotocol.dev/introduction/welcome
- ACP repository: https://github.com/i-am-bee/acp
- ACP OpenAPI spec (raw): https://raw.githubusercontent.com/i-am-bee/acp/main/docs/spec/openapi.yaml
