---
id: ELITEA-2931
title: "Pipeline Toolkit node: two sequential Toolkit nodes each requiring auth for a different toolkit resolve independently and in order"
priority: high
type: integration
module: toolkit-authorization
status: draft
execution_type: manual
tags: [feat:mcp-remote, feat:toolkits, int:openapi, int:sharepoint, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6072]
---

## Preconditions

- User is logged in to `{{base_url}}`
- A pipeline exists with Toolkit node 1 (SharePoint, delegated mode, no token) followed in sequence by Toolkit node 2 (OpenAPI, OAuth Delegated, no token)

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Pipeline structure | Toolkit node 1 (SharePoint) → Toolkit node 2 (OpenAPI), sequential |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Run the pipeline | Run starts and pauses at Toolkit node 1 |
| 2 | Confirm the popup for Toolkit node 1 appears first, then Authorize it | Toolkit node 1's tool call executes |
| 3 | Observe the pipeline advancing | Pipeline advances to Toolkit node 2; its popup then appears |
| 4 | Authorize the popup for Toolkit node 2 | Toolkit node 2's tool call executes |
| 5 | Observe pipeline completion | Pipeline completes using both nodes' outputs |

## Expected Final State

Both Toolkit node authorization popups appeared in the correct sequential order, were resolved independently, and the pipeline completed using both nodes' outputs — neither popup was skipped, merged, or shown out of order.

## Pass/Fail Criteria

**Pass:**
- Popups for Toolkit node 1 and node 2 appear strictly in pipeline order
- Both nodes execute correctly and pipeline completes using both outputs

**Fail:**
- Popups appear out of order, are merged into one, or one is silently skipped
- Pipeline completes without correctly using the output of one or both Toolkit nodes
