---
id: ELITEA-3189
title: "Remote MCP: changing max tool description length on an existing toolkit picks up the new cap on next tool discovery"
priority: medium
type: functional
module: mcp-servers
status: draft
execution_type: manual
tags: [feat:mcp, feat:mcp-remote, r-2.0.6, issue:6016]
requirements: [EliteaAI/elitea_issues#6016]
---
# ELITEA-3189: Updated Cap Applies on Next Discovery

**Module:** Mcp Servers · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that changing `Maximum tool description length` on an already-configured Remote MCP toolkit is picked up the next time tools are (re)discovered — without requiring a full server restart or unrelated workaround.

## Preconditions

- User is logged into Elitea platform
- A Remote MCP toolkit is already configured and connected, with at least one tool whose description exceeds 1000 characters
- User has permission to edit the toolkit's configuration

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | With no cap configured, add the toolkit to an agent and confirm the long tool's description is exposed in full | Full, untruncated description observed |
| 2 | Edit the toolkit and set `Maximum tool description length` to `200` and save | Save succeeds |
| 3 | Re-add the toolkit to the agent (or refresh/reconnect tools) without changing anything else | Tool discovery re-runs |
| 4 | Inspect the long tool's description again | Now shortened to at most 200 characters, per the new cap |
| 5 | Edit the toolkit again, clear the field (back to unlimited), save, and re-trigger discovery | Description returns to its full, untruncated form |

## Expected Final State

The configured cap is live — each change is reflected the next time tools are discovered, both when tightening and when loosening/removing the cap.

## Pass/Fail Criteria

**Pass:** Description length reflects the currently configured cap after each change and re-discovery.
**Fail:** An old cap value persists after being changed, or a new cap is not applied without an unrelated workaround (e.g. full service restart).
