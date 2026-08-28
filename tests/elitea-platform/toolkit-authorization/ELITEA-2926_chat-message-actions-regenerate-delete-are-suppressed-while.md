---
id: ELITEA-2926
title: "Chat message actions (regenerate/delete) are suppressed while a toolkit-authorization popup is pending"
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
- An OAuth-requiring toolkit (no valid token) is available and addable to a chat

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Toolkit under test | Any OAuth-requiring toolkit (SharePoint/OpenAPI/Remote MCP) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Send a message that triggers the "Toolkit Authorization Required" popup | Popup appears on the relevant message |
| 2 | While the popup is pending, inspect the message for regenerate and delete controls | No regenerate and no delete buttons are present on the auth popup message |
| 3 | Resolve the popup (click Authorize or Skip) | Popup resolves and the tool call completes/cancels accordingly |
| 4 | Inspect the resulting last LLM message | Regenerate and delete buttons are present and functional on the last LLM message |

## Expected Final State

Regenerate/delete controls remain hidden for the duration the toolkit-authorization popup is pending, and reappear correctly on the last LLM message once the popup is resolved.

## Pass/Fail Criteria

**Pass:**
- No regenerate/delete controls visible on the message while the popup is pending
- Regenerate/delete controls are present and functional after resolution, on the appropriate message

**Fail:**
- Regenerate or delete controls are visible/clickable while the popup is still pending
- Regenerate/delete controls fail to reappear after the popup resolves
