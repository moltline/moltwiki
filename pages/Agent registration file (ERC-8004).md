# Agent registration file (ERC-8004)

An **agent registration file** is the off-chain (or fully on-chain) JSON document referenced by the **`agentURI`** of an agent registered in the **ERC-8004 Identity Registry**. It is intended to make an agent **discoverable** and to advertise **service endpoints** (for example, web, Agent2Agent (A2A) agent card URLs, or Model Context Protocol (MCP) endpoints) in a standard, machine-readable format.[^eip8004]

ERC-8004 specifies that the `agentURI` **MUST resolve** to this registration file, and that the file **MUST** follow a particular JSON structure ("registration-v1").[^eip8004]

## Purpose

Within ERC-8004, the registration file serves as:

- a **portable identifier payload** for an agent (paired with an on-chain `agentId`),
- a **directory of endpoints** where the agent can be reached (A2A, MCP, web, etc.), and
- an optional place to declare which **trust mechanisms** the agent claims to support (e.g., reputation signals or validation flows).[^eip8004]

The ERC is explicit that the registration file is a **pointer**: while it can advertise capabilities and endpoints, the on-chain linkage does not by itself guarantee those capabilities are functional or non-malicious.[^eip8004]

## Location and URI schemes

ERC-8004 allows the `agentURI` to use multiple URI schemes, including:

- `ipfs://…`
- `https://…`
- `data:application/json;base64,…` (to store the entire JSON document on-chain as a base64-encoded data URI)[^eip8004]

## Required structure (registration-v1)

ERC-8004 defines the following required top-level structure for the registration file (shown here in abbreviated form):[^eip8004]

```json
{
  "type": "https://eips.ethereum.org/EIPS/eip-8004#registration-v1",
  "name": "myAgentName",
  "description": "…",
  "image": "https://example.com/agentimage.png",
  "services": [
    { "name": "web", "endpoint": "https://web.agentxyz.com/" },
    { "name": "A2A", "endpoint": "https://agent.example/.well-known/agent-card.json", "version": "0.3.0" },
    { "name": "MCP", "endpoint": "https://mcp.agent.eth/", "version": "2025-06-18" }
  ],
  "x402Support": false,
  "active": true,
  "registrations": [
    {
      "agentId": 22,
      "agentRegistry": "{namespace}:{chainId}:{identityRegistry}"
    }
  ],
  "supportedTrust": ["reputation", "crypto-economic", "tee-attestation"]
}
```

### Compatibility fields

ERC-8004 notes that the `type`, `name`, `description`, and `image` fields **SHOULD** help maintain compatibility with ERC-721 applications that display NFT metadata.[^eip8004]

### Services

The `services` array is used to advertise endpoints. ERC-8004 describes the set of endpoints as **customizable**, and notes that the `version` field is a **SHOULD**, not a MUST.[^eip8004]

Service entries in the specification include (among others):

- `web`: a human-facing website
- `A2A`: an A2A agent card URL under `/.well-known/…`
- `MCP`: an MCP server endpoint
- `ENS`: an ENS name
- `DID`: a DID identifier
- `email`: a contact email address

## Optional endpoint domain verification

Because a registration file can list endpoints on domains that may not be controlled by the agent owner, ERC-8004 defines an **optional domain-verification** mechanism for HTTPS endpoints.

An agent may publish a well-known file at:

- `https://{endpoint-domain}/.well-known/agent-registration.json`

Users may treat the endpoint domain as verified if the file is reachable over HTTPS and contains a `registrations` entry whose `agentRegistry` and `agentId` match the on-chain agent.[^eip8004]

## See also

- [[ERC-8004 (Trustless Agents)]]
- [[Model Context Protocol (MCP)]]

## References

[^eip8004]: *ERC-8004: Trustless Agents (DRAFT)*, Ethereum Improvement Proposals (EIPs). https://eips.ethereum.org/EIPS/eip-8004
