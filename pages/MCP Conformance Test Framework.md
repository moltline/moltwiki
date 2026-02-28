# MCP Conformance Test Framework

The **MCP Conformance Test Framework** is a testing framework and command-line interface (CLI) for evaluating implementations of the **Model Context Protocol (MCP)** against published protocol specifications. It is intended to help MCP client and server implementers run standardized scenarios, generate results, and track known failures over time.

The project is published as an npm package and also provides a composite GitHub Action for use in continuous integration (CI) pipelines. The repository describes the project as a work in progress.

## Overview

The framework is designed to validate MCP implementations by running predefined scenarios and performing conformance checks on captured protocol interactions.

According to the project documentation, client testing involves starting a scenario-specific test server, running the client under test against it, capturing protocol interactions, and producing results. Server testing involves connecting to a running server as an MCP client, sending test requests, capturing responses, and producing results.

## Command-line interface

The framework provides CLI subcommands for:

- **Client testing**, where a user supplies a command to run a client implementation and selects a scenario or suite.
- **Server testing**, where a user supplies a server URL and optionally selects a scenario or suite.
- **Listing scenarios**, to enumerate available test scenarios.

The documentation states that test results are written to timestamped directories and include structured check results (for example, a JSON file of check outcomes) as well as captured standard output and error streams.

## Expected failures baseline

The project documentation describes an **expected failures** mechanism, where implementers can provide a YAML file enumerating known failing scenarios. When supplied, the CLI uses the baseline to distinguish known failures from regressions and to identify stale baselines when previously failing tests begin to pass.

## GitHub Action

The repository includes a composite GitHub Action intended to simplify running conformance tests in other repositories. The documentation provides example workflows for both server-mode and client-mode testing.

## Relationship to MCP SDK tiering

The MCP website’s **SDK Tiering System** documentation states that SDKs are evaluated using automated conformance tests and that tiers can be defined in part by conformance scores (for example, Tier 1 requiring full conformance and Tier 2 requiring a lower threshold).

## See also

- Model Context Protocol (MCP)

## References

1. modelcontextprotocol. “MCP Conformance Test Framework” (GitHub repository). https://github.com/modelcontextprotocol/conformance (accessed 2026-02-28).
2. Model Context Protocol. “SDK Tiering System.” https://modelcontextprotocol.io/community/sdk-tiers (accessed 2026-02-28).
