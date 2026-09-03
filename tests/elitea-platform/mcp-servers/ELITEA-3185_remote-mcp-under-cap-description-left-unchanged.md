---
id: ELITEA-3185
title: "Remote MCP: a tool description already under the configured cap is left completely unchanged"
priority: medium
type: functional
module: mcp-servers
status: draft
execution_type: manual
tags: [feat:mcp, feat:mcp-remote, r-2.0.6, issue:6016]
requirements: [EliteaAI/elitea_issues#6016]
---
# ELITEA-3185: Under-Cap Description Is Unchanged

**Module:** Mcp Servers · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that when a tool's description (plus toolkit attribution) is already shorter than the configured `Maximum tool description length`, the description is passed through unmodified — no shortening, no trailing `...` added.

## Preconditions

- User is logged into Elitea platform
- A Remote MCP toolkit is configured and connected to an external MCP server exposing at least one tool with a short description (well under 1000 characters)
- User has permission to edit the toolkit's configuration

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Open the Remote MCP toolkit's configuration and set `Maximum tool description length` to a value comfortably larger than the short tool's description + attribution (e.g. `500`) | Value is accepted and saved |
| 2 | Trigger tool discovery (add to an agent / refresh tools) | Tools reload without error |
| 3 | Inspect the short tool's description | Text matches the original MCP server description plus attribution, exactly |
| 4 | Confirm no `...` was appended | Description does not end in `...` unless the original source text itself ended that way |

## Expected Final State

Descriptions under the configured cap are byte-for-byte unchanged aside from the standard toolkit attribution line that is always appended.

## Pass/Fail Criteria

**Pass:** Under-cap description is identical to the unshortened source text plus attribution.
**Fail:** Any shortening or trailing `...` is applied to a description that was already under the cap.
