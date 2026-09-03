---
id: ELITEA-3190
title: "Remote MCP: description cap applies consistently on toolkit reconnect and to MCP server-exposed prompts"
priority: low
type: functional
module: mcp-servers
status: draft
execution_type: manual
tags: [feat:mcp, feat:mcp-remote, r-2.0.6, issue:6016]
requirements: [EliteaAI/elitea_issues#6016]
---
# ELITEA-3190: Cap Consistency Across Reconnect and Prompts

**Module:** Mcp Servers · **Priority:** Low · **Type:** Functional

**Objective:** Verify the configured `Maximum tool description length` applies the same way whether tools are created via a fresh live connection or via reconnecting to an already-configured toolkit, and that it also applies to MCP server-exposed prompts (which the SDK converts into tools), not just ordinary MCP tools.

## Preconditions

- User is logged into Elitea platform
- A Remote MCP toolkit is configured with a cap set (e.g. `240`), connected to a server exposing both a long-description tool and at least one server-side prompt
- User has permission to edit/reconnect the toolkit

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | With the cap already set, connect the toolkit fresh (new agent/new chat) and inspect the long tool's description | Description is shortened per the cap, attribution intact |
| 2 | Disconnect and reconnect the same toolkit in an existing conversation where it was already used before (exercising the reconnect/static path) | Tools reload without error |
| 3 | Inspect the same tool's description after reconnect | Shortened identically to step 1 — same length/cut point, no discrepancy between fresh and reconnected discovery |
| 4 | Inspect a tool derived from one of the server's exposed prompts, if its underlying prompt text exceeds the cap | Prompt-derived tool's description is also shortened per the same cap and attribution rules as ordinary tools |

## Expected Final State

Description shortening behaves identically regardless of discovery path, and covers prompt-derived tools as well as ordinary tools.

## Pass/Fail Criteria

**Pass:** Same tool produces an identically-shortened description on fresh vs. reconnect discovery; prompt-derived tools are capped the same way.
**Fail:** Fresh and reconnected discovery disagree on the shortened description, or prompt-derived tools bypass the cap entirely.
