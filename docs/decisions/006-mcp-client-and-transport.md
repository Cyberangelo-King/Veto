# ADR 006 — Self-hosted MCP server and real web MCP client

- **Status:** Accepted
- **Date:** 2026-10-14
- **Decision owner:** Product owner

## Context
The Alexa+ track's official requirements specify a working Agent Skill or a self-hosted MCP server using MCP specification 2025-11-25 or later over Streamable HTTP. The official FAQ says the gated Alexa+ developer tools (Category SDK, MCP Toolkit, CLI, and Web Simulator) are preview-only and unavailable to hackathon participants; the FAQ directs builders to demo through their own web-based simulator or front end.

## Decision
Build a self-hosted TypeScript MCP server using the selected @modelcontextprotocol/sdk package at a compatible pinned version. Implement Streamable HTTP for MCP spec revision 2025-11-25 or later. Build a web voice client that is itself a real MCP client and connects to the server through MCP protocol traffic.

The web client must initialize the MCP session/capabilities, discover and invoke tools through the MCP client/transport, and render returned tool results. It must not directly call hidden business functions or ordinary REST endpoints as a substitute for MCP tool invocation. Speech recognition and playback are user-interface adapters around the MCP client, not replacements for the protocol.

Veto does not claim to connect live to the Alexa+ assistant. The working target is the self-hosted MCP integration plus a web voice experience that demonstrates the same intended assistant workflow.

## Consequences
- MCP is a real application boundary with typed tools, error contracts, authorization, and tests.
- The web client can be used locally without access to the gated Alexa+ preview tools.
- The selected SDK version and Lambda front-door adapter must be proven compatible with the required protocol revision and Streamable HTTP semantics.
- CORS, browser transport support, session headers, request cancellation, and identity handling must be tested.
- The demo must clearly identify the web voice client as Veto's client, not a live Alexa+ assistant.

## Revisit
Only if the official event requirements change or an approved Alexa+ integration becomes available. Any change to protocol/transport requires a new decision and compatibility tests.
