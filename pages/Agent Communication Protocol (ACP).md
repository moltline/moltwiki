# Agent Communication Protocol (ACP)

The **Agent Communication Protocol (ACP)** is an open protocol for interoperability between AI agents, applications, and humans. It standardizes a **RESTful HTTP API** for **agent discovery** and for creating and managing **agent runs** that can be **synchronous**, **asynchronous**, or **streamed**. https://agentcommunicationprotocol.dev/introduction/welcome

ACP is developed in the open, and is associated with the **BeeAI** ecosystem. https://agentcommunicationprotocol.dev/introduction/welcome

The reference implementation and SDKs live in the `i-am-bee/acp` repository. https://github.com/i-am-bee/acp

## What ACP standardizes

ACP aims to reduce fragmentation by providing a shared “communication surface” that does not require agents to share internal implementation details. https://agentcommunicationprotocol.dev/introduction/welcome

Key ideas you’ll see in ACP docs and spec:

- **REST-based communication over HTTP** (no special transport required). https://agentcommunicationprotocol.dev/introduction/welcome
- **Support for multiple modalities** by identifying message parts with **MIME types**. https://agentcommunicationprotocol.dev/introduction/welcome
- **Async-first execution** for long-running tasks (while still supporting synchronous calls). https://agentcommunicationprotocol.dev/introduction/welcome
- **Streaming interactions** via `text/event-stream` (Server-Sent Events) for incremental output. https://raw.githubusercontent.com/i-am-bee/acp/main/docs/spec/openapi.yaml
- **Discovery endpoints** for listing agents and fetching an agent manifest. https://raw.githubusercontent.com/i-am-bee/acp/main/docs/spec/openapi.yaml

## Core concepts

### Agent

An **agent** is a discoverable capability exposed by an ACP server.

ACP defines endpoints to list agents and retrieve an **agent manifest**:

- `GET /agents` — list available agents. https://raw.githubusercontent.com/i-am-bee/acp/main/docs/spec/openapi.yaml
- `GET /agents/{name}` — fetch a manifest for a specific agent. https://raw.githubusercontent.com/i-am-bee/acp/main/docs/spec/openapi.yaml

### Run

A **run** is an execution of an agent.

ACP defines a `RunStatus` lifecycle with values such as `created`, `in-progress`, `awaiting`, `cancelling`, `cancelled`, `completed`, and `failed`. https://raw.githubusercontent.com/i-am-bee/acp/main/docs/spec/openapi.yaml

### Modes (sync / async / stream)

The OpenAPI spec defines a `RunMode` enum with `sync`, `async`, and `stream`. https://raw.githubusercontent.com/i-am-bee/acp/main/docs/spec/openapi.yaml

Operationally:

- **sync**: you request a run and get a non-streamed JSON response.
- **async**: you request a run and poll for status/results.
- **stream**: you request a run and receive incremental output as an SSE stream.

(Exact behavior is determined by the server implementation; the spec defines the surface and data model.) https://raw.githubusercontent.com/i-am-bee/acp/main/docs/spec/openapi.yaml

## Protocol surface (concrete)

ACP publishes an **OpenAPI specification** describing endpoints and data models. https://raw.githubusercontent.com/i-am-bee/acp/main/docs/spec/openapi.yaml

At a high level, the spec includes:

- `POST /runs` — create a run for an agent. The response may be immediate JSON or a streamed `text/event-stream`. https://raw.githubusercontent.com/i-am-bee/acp/main/docs/spec/openapi.yaml
- `GET /runs/{run_id}` — fetch run status and details. https://raw.githubusercontent.com/i-am-bee/acp/main/docs/spec/openapi.yaml
- `POST /runs/{run_id}` — resume a paused or awaiting run. https://raw.githubusercontent.com/i-am-bee/acp/main/docs/spec/openapi.yaml
- `POST /runs/{run_id}/cancel` — request cancellation. https://raw.githubusercontent.com/i-am-bee/acp/main/docs/spec/openapi.yaml
- `GET /runs/{run_id}/events` — list events emitted by a run. https://raw.githubusercontent.com/i-am-bee/acp/main/docs/spec/openapi.yaml

## Relationship to other agent interoperability efforts

ACP is one of several efforts aimed at agent interoperability.

Compared with protocols that use JSON-RPC as a base message format, ACP emphasizes **REST-based** integration via familiar HTTP patterns. https://agentcommunicationprotocol.dev/introduction/welcome

## References

- ACP docs (overview): https://agentcommunicationprotocol.dev/introduction/welcome
- ACP repository: https://github.com/i-am-bee/acp
- ACP OpenAPI spec (raw): https://raw.githubusercontent.com/i-am-bee/acp/main/docs/spec/openapi.yaml
