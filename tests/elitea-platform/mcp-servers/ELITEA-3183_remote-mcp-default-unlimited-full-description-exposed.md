---
id: ELITEA-3183
title: "Remote MCP: default (unset) max tool description length exposes long descriptions in full, no 1000-char cutoff"
priority: high
type: functional
module: mcp-servers
status: draft
execution_type: manual
tags: [feat:mcp, feat:mcp-remote, r-2.0.6, issue:6016]
requirements: [EliteaAI/elitea_issues#6016]
---
# ELITEA-3183: Remote MCP Default Is Unlimited Description Length

**Module:** Mcp Servers · **Priority:** High · **Type:** Functional

**Objective:** Verify that with no `Maximum tool description length` value configured (default/unset, i.e. `0`) on a Remote MCP toolkit, a tool whose description from the MCP server exceeds 1000 characters is exposed to the agent in full and unmodified — the previous hard 1000-character truncation no longer applies.

## Preconditions

- User is logged into Elitea platform
- A Remote MCP toolkit (Toolkits → MCPs, connecting to an external MCP server by URL, `type: mcp`) is configured and connected
- The connected MCP server exposes at least one tool whose description is longer than 1000 characters
- `Maximum tool description length` field on the toolkit is left empty/default

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Open the Remote MCP toolkit's configuration and confirm `Maximum tool description length` is empty/unset | Field shows no value (default) |
| 2 | Add the toolkit to an agent (or open it directly in chat) and trigger tool discovery | Tools load without error |
| 3 | Inspect the full description of the tool known to exceed 1000 characters (via the tool's detail view, an API/trace call that returns the tool definition, or by having the agent recite the tool's description back) | The complete description text is present, with no cutoff and no trailing `...` inserted mid-sentence |
| 4 | Confirm the description length is not capped at exactly 1000 characters (or 997 + `...`) | Description length matches the source MCP server's original text, not truncated to the old hard limit |

## Expected Final State

The tool's description reaches the agent exactly as published by the MCP server, regardless of length, when no cap is configured.

## Pass/Fail Criteria

**Pass:** Full, untruncated description (>1000 chars) is exposed with no cutoff.
**Fail:** Description is cut at or near 1000 characters, or ends with an unexpected `...` not present in the source text.
