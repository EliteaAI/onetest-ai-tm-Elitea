---
id: ELITEA-2934
title: "Pipeline Pipeline node: nested sub-pipeline with multiple Toolkit nodes requiring sequential auth resolves fully before parent proceeds"
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
- A parent pipeline contains a Pipeline node invoking a sub-pipeline
- The sub-pipeline contains two or more Toolkit nodes in sequence, each requiring delegated auth for a different toolkit, no valid tokens

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Pipeline structure | Parent pipeline → Pipeline node → sub-pipeline → Toolkit node A → Toolkit node B (sequential, both auth required) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Run the parent pipeline | Run proceeds into the Pipeline node, entering the sub-pipeline |
| 2 | Observe and Authorize the popup for sub-pipeline Toolkit node A | Node A's tool call executes; sub-pipeline advances to Toolkit node B |
| 3 | Observe and Authorize the popup for sub-pipeline Toolkit node B | Node B's tool call executes |
| 4 | Observe the parent pipeline after the sub-pipeline finishes | Parent pipeline only proceeds past the Pipeline node after BOTH nested authorizations are fully resolved |

## Expected Final State

The parent pipeline does not proceed past the Pipeline node until every Toolkit node inside the nested sub-pipeline has had its authorization resolved, in correct sequence.

## Pass/Fail Criteria

**Pass:**
- Both nested Toolkit node popups surface and resolve in correct sequence
- Parent pipeline only continues after the sub-pipeline (and all its nested authorizations) fully completes

**Fail:**
- Parent pipeline proceeds prematurely, before all nested authorizations are resolved
- One of the nested popups is skipped, merged, or never surfaces
