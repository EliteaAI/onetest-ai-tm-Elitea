---
id: ELITEA-2921
title: "Toolkit Authorization Required popup renders and blocks tool execution when OAuth is missing or expired"
priority: critical
type: functional
module: toolkit-authorization
status: draft
execution_type: manual
tags: [feat:mcp-remote, feat:toolkits, int:openapi, int:sharepoint, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6072]
---

## Preconditions

- User is logged in to `{{base_url}}`
- A SharePoint credential exists with Authentication tab = **Delegated (User OAuth)** (Client ID, Client Secret, Site URL, OAuth Discovery Endpoint `https://login.microsoftonline.com/{tenant_id}`, Scopes e.g. `Sites.ReadWrite.All`), no valid token yet, and a SharePoint toolkit built on it
- An OpenAPI credential of type "OpenAPI Configuration" with Authentication Method = **OAuth (Delegated)**, no valid token yet, and an OpenAPI toolkit built on it
- A Remote MCP server requiring OAuth (e.g. Atlassian Remote MCP) with no active session
- A chat conversation exists with each toolkit added as a participant, one at a time for this test

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Toolkit types under test | SharePoint (Delegated), OpenAPI (OAuth Delegated), Remote MCP (Atlassian) |
| Trigger message — SharePoint | "list files in Shared Documents" |
| Trigger message — OpenAPI | Any request invoking the OpenAPI-defined operation |
| Trigger message — Remote MCP | A request invoking an Atlassian tool such as `mcp_auth_control` / `mcp_authorize_Atlassian` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Add the SharePoint toolkit (delegated, no token) as the sole participant in a new chat and send the SharePoint trigger message | "Toolkit Authorization Required" popup appears; the underlying tool call is paused, not executed |
| 2 | Inspect the popup's Authorization details | Toolkit server, Resource metadata, Authorization server, and Scopes fields are populated with the SharePoint credential's OAuth Discovery Endpoint and configured scopes |
| 3 | Repeat steps 1–2 with the OpenAPI toolkit (delegated, no token) and its trigger message | Popup appears with fields populated from the OpenAPI credential's Oauth Discovery Endpoint and Scope; tool call is paused |
| 4 | Repeat steps 1–2 with the Remote MCP toolkit (no active session) and its trigger message | Popup appears with fields populated from the MCP server URL/metadata; tool call is paused |
| 5 | For each of the three cases, wait without clicking Authorize or Skip | The underlying tool never executes and no result streams until a decision is made |

## Expected Final State

For all three toolkit types (SharePoint, OpenAPI, Remote MCP), the "Toolkit Authorization Required" popup is displayed with toolkit-specific Authorization details populated, and the originating tool call remains paused and unexecuted until the user acts on the popup.

## Pass/Fail Criteria

**Pass:**
- Popup renders for all three toolkit types when OAuth is missing/expired
- Toolkit server, Resource metadata, Authorization server, and Scopes are correctly populated per toolkit
- No tool execution occurs prior to Authorize/Skip

**Fail:**
- Popup fails to appear for any toolkit type requiring delegated auth
- Authorization details fields are empty, generic, or mismatched to the toolkit
- The underlying tool executes before the popup is resolved
