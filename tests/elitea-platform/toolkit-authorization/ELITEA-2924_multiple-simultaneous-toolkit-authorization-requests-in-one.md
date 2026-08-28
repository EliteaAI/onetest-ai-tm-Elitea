---
id: ELITEA-2924
title: "Multiple simultaneous toolkit-authorization requests in one turn are each surfaced and resolved independently"
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
- A chat conversation has 2+ OAuth-requiring toolkits/MCPs as participants, none with a valid token

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Participants | 2+ OAuth-requiring toolkits/MCPs (e.g. SharePoint delegated + Remote MCP) |
| Trigger message | A single message that invokes tools from both toolkits in the same turn |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Send a message causing 2+ toolkits to require authorization in the same turn | A separate "Toolkit Authorization Required" popup/request is surfaced for each toolkit (sequentially or stacked) |
| 2 | Click **Authorize** on the first request only | First request completes and resumes its tool call; second request remains pending and separately actionable |
| 3 | Click **Skip** on the second, still-pending request | Second request is cancelled; first request's earlier resolution is unaffected |
| 4 | Review both outcomes | One toolkit executed successfully (from Authorize), the other was skipped — with no cross-contamination between the two |

## Expected Final State

Both authorization requests from the same turn were surfaced and resolved fully independently: the authorized toolkit executed and returned a result, the skipped toolkit did not execute, and neither resolution affected the other.

## Pass/Fail Criteria

**Pass:**
- All simultaneous authorization requests from one turn are surfaced, none dismissed automatically
- Resolving one request does not auto-resolve or dismiss any other pending request
- Final state correctly reflects independent Authorize/Skip outcomes per toolkit

**Fail:**
- A second/later request is silently dismissed when the first is resolved
- Resolving one request incorrectly resolves or affects another
- Only one of multiple simultaneous requests is ever surfaced
