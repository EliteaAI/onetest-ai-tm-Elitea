---
id: ELITEA-3184
title: "Remote MCP: positive max tool description length shortens at a clean boundary and preserves toolkit attribution"
priority: high
type: functional
module: mcp-servers
status: draft
execution_type: manual
tags: [feat:mcp, feat:mcp-remote, r-2.0.6, issue:6016]
requirements: [EliteaAI/elitea_issues#6016]
---
# ELITEA-3184: Positive Cap Shortens Cleanly and Keeps Attribution

**Module:** Mcp Servers · **Priority:** High · **Type:** Functional

**Objective:** Verify that configuring a positive `Maximum tool description length` (e.g. `240`) on a Remote MCP toolkit shortens a tool description that exceeds it to at most that many characters, cutting at a sentence/line/word boundary rather than mid-word, ending in `...`, while the `Toolkit: <name>` (and, where applicable, `(<url>)`) attribution line stays intact at the end.

## Preconditions

- User is logged into Elitea platform
- A Remote MCP toolkit is configured and connected to an external MCP server exposing a tool whose description (plus toolkit attribution) exceeds 240 characters
- User has permission to edit the toolkit's configuration

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Open the Remote MCP toolkit's configuration and set `Maximum tool description length` to `240` | Value is accepted |
| 2 | Save the toolkit and trigger tool discovery (add to an agent / refresh tools) | Tools reload without error |
| 3 | Inspect the description of the tool known to exceed the cap | Description is at most 240 characters |
| 4 | Check where the description was cut | The cut lands at a sentence, newline, or word boundary — no word is split mid-character |
| 5 | Check the end of the shortened description | Ends in `...` |
| 6 | Check for the toolkit attribution (`Toolkit: <name>`, or `Toolkit: <name> (<url>)` for directly-discovered remote tools) | Attribution line is present and fully intact at the end of the description, not itself cut off |

## Expected Final State

The tool's agent-facing description is shortened to the configured cap at a readable boundary, with the toolkit attribution still fully readable.

## Pass/Fail Criteria

**Pass:** Description ≤ configured cap, cut at a clean boundary, ends in `...`, attribution line fully present.
**Fail:** Description exceeds the cap, is cut mid-word, is missing the trailing `...`, or the attribution line is itself truncated/missing.
