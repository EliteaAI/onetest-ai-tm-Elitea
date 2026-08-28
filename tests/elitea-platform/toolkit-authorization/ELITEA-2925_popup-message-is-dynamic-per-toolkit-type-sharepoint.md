---
id: ELITEA-2925
title: "Popup message is dynamic per toolkit type (SharePoint / OpenAPI / Remote MCP) instead of generic server-URL text"
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
- SharePoint (delegated), OpenAPI (delegated), and Remote MCP toolkits are each available and addable to a chat, none with a valid token

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Toolkit types | SharePoint, OpenAPI, Remote MCP |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Trigger the popup from the SharePoint toolkit and record the primary message and "Authorization details" wording | Message/content reflects SharePoint context, not the generic `Authorization is required for toolkit "<url>"` text |
| 2 | Trigger the popup from the OpenAPI toolkit and record the same | Message/content reflects OpenAPI context |
| 3 | Trigger the popup from the Remote MCP toolkit and record the same | Message/content reflects Remote MCP context |
| 4 | Compare the three recorded messages | Each is worded appropriately for its toolkit type; none are identical generic boilerplate across all three |

## Expected Final State

Each of the three toolkit types produces a popup message contextualized to that toolkit type, rather than an identical generic server-URL string shared across all types.

## Pass/Fail Criteria

**Pass:**
- SharePoint, OpenAPI, and Remote MCP popups each show distinct, contextually appropriate wording
- No toolkit type falls back to the old generic `Authorization is required for toolkit "<url>"` text

**Fail:**
- Any toolkit type still shows the old generic message
- All three toolkit types show identical wording with no type-specific context
