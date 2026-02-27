# MCP Registry Aggregators

An **MCP Registry aggregator** is a downstream consumer of the **Model Context Protocol (MCP) Registry** that ingests registry data and provides additional value (for example, a marketplace with user ratings and security scanning). Aggregators typically scrape the MCP Registry’s read-only REST API periodically and persist the results in their own datastore.

## Overview

The MCP documentation describes aggregators as "downstream consumers" of the registry that can build services on top of registry metadata. The MCP Registry API is described as **unauthenticated** and **read-only**, and the registry does not provide uptime or data durability guarantees, so aggregators are expected to store their own copies of the data.\[1]

## MCP Registry REST API (for aggregators)

The MCP documentation lists the following endpoints for consuming registry data:\[1]

- `GET /v0.1/servers` — list servers
- `GET /v0.1/servers/{serverName}/versions` — list versions of a server
- `GET /v0.1/servers/{serverName}/versions/{version}` — fetch a specific server version (including the special version `latest`)

### Pagination

The `GET /v0.1/servers` endpoint supports cursor-based pagination using `limit` and `cursor` query parameters.\[1]

### Filtering by update time

The same endpoint supports filtering servers updated since a given timestamp using an `updated_since` query parameter in RFC 3339 date-time format.\[1]\[2]

## Subregistries

A **subregistry** is an aggregator that also implements the OpenAPI specification defined by the MCP Registry, allowing MCP clients (such as host applications) to consume server metadata via a standardized interface. The documentation notes that subregistries may add custom metadata via an `_meta` field (for example, ratings, download counts, or security scan results).\[1]

## References

1. Model Context Protocol. "MCP Registry Aggregators." https://modelcontextprotocol.io/registry/registry-aggregators
2. IETF. *RFC 3339: Date and Time on the Internet: Timestamps.* https://datatracker.ietf.org/doc/html/rfc3339
