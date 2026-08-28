---
id: ELITEA-2929
title: "Skip does not desynchronize the PARTICIPANTS panel disconnected/reconnect indicator for the affected MCP"
priority: high
type: functional
module: toolkit-authorization
status: draft
execution_type: manual
tags: [feat:mcp-remote, feat:toolkits, int:openapi, int:sharepoint, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6072]
---

## Preconditions

- User is logged in to `{{base_url}}`
- An OAuth-requiring Remote MCP (no active session) is added as a chat participant, with the PARTICIPANTS panel visible

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| MCP under test | An OAuth-requiring Remote MCP (e.g. Atlassian) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Trigger the "Toolkit Authorization Required" popup for the MCP | Popup appears |
| 2 | Click **Skip** | Popup resolves as skipped, tool call not executed |
| 3 | Open the PARTICIPANTS panel and check the entry for that MCP | Entry correctly shows "disconnected" / "Log in" state matching the skipped/unauthenticated status |
| 4 | Click "Log in" from the PARTICIPANTS panel entry | The same authorization flow is re-triggered correctly (popup or OAuth flow reopens as expected) |

## Expected Final State

After a Skip, the PARTICIPANTS panel accurately reflects the MCP's disconnected state, and its "Log in" affordance correctly re-triggers the authorization flow.

## Pass/Fail Criteria

**Pass:**
- PARTICIPANTS panel shows correct disconnected/"Log in" state after Skip
- Clicking "Log in" from the panel correctly re-triggers authorization

**Fail:**
- PARTICIPANTS panel shows a stale/incorrect connection state after Skip
- "Log in" from the panel fails to re-trigger authorization or triggers the wrong flow
