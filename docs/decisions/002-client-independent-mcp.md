# ADR 002 — Initial client-independent MCP exploration

- **Status:** Superseded by ADR 006
- **Date:** 2026-10-14
- **Owner:** Product owner

## Context
The initial repository bootstrap left the final client/integration path open pending official platform evidence. This record preserves the initial exploration rather than remaining an active proposal.

## Initial direction
The project should keep its tools independent of the client and use a web simulator if a direct Alexa+ integration could not be verified.

## Resolution
Official hackathon rules and FAQ have now been reviewed. The accepted path is in ADR 006: a self-hosted TypeScript MCP server using MCP 2025-11-25 or later over Streamable HTTP, plus a web voice client that uses a real MCP client to call the server. The project does not claim a live connection into the Alexa+ assistant because the gated Alexa+ developer tools are unavailable to hackathon participants.

ADR 007 locks the AWS and local runtime target.

## Historical note
Do not treat this ADR's former “proposed” status as the current architecture. ADRs 006 and 007 are the active decisions; protocol, SDK, and runtime behavior still require implementation tests.
