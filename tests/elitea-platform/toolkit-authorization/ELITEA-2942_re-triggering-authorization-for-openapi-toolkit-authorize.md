---
id: ELITEA-2942
title: "Re-triggering authorization for OpenAPI toolkit (Authorize and Skip flows) is covered end-to-end"
priority: medium
type: functional
module: toolkit-authorization
status: draft
execution_type: manual
tags: [feat:mcp-remote, feat:toolkits, int:openapi, int:sharepoint, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6072]
---

## Preconditions

- User is logged in to `{{base_url}}`
- An OpenAPI credential of type "OpenAPI Configuration" with Authentication Method = OAuth (Delegated), no valid token, and an OpenAPI toolkit built on it, added to a chat

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Toolkit under test | OpenAPI (OAuth Delegated) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Send a message invoking the OpenAPI toolkit's operation | "Toolkit Authorization Required" popup appears |
| 2 | Click **Skip** | Toolkit call is not executed; conversation remains usable |
| 3 | Send another message invoking the same OpenAPI toolkit's operation again | Popup re-triggers correctly (re-surfaces the authorization requirement, no stale/cached bypass) |
| 4 | Click **Authorize** and complete OAuth | Toolkit call executes and streams a result |
| 5 | Send another message invoking the same toolkit's operation once the token is valid | No popup appears; tool executes directly using the now-valid token |

## Expected Final State

Re-triggering authorization for the OpenAPI toolkit correctly surfaces the popup again after a Skip, correctly completes via Authorize, and does not re-prompt once a valid token exists.

## Pass/Fail Criteria

**Pass:**
- Popup correctly re-triggers after a prior Skip on subsequent invocation
- Authorize completes OAuth and the tool executes with a streamed result
- Once authorized, subsequent calls execute directly without re-prompting

**Fail:**
- Popup fails to re-trigger after a Skip (tool silently fails or executes without auth)
- Tool continues prompting for authorization even after a valid token exists
