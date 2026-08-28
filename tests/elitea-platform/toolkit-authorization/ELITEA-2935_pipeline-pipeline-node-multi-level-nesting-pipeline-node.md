---
id: ELITEA-2935
title: "Pipeline Pipeline node: multi-level nesting (Pipeline node → sub-pipeline → another Pipeline node) preserves correct auth attribution"
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
- A top-level pipeline contains a Pipeline node invoking sub-pipeline A, which itself contains another Pipeline node invoking sub-pipeline B
- Sub-pipeline B contains a Toolkit node calling a delegated toolkit with no valid token

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Pipeline structure | Top-level pipeline → Pipeline node → sub-pipeline A → Pipeline node → sub-pipeline B → Toolkit node (auth required) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Run the top-level pipeline | Run proceeds through the first Pipeline node into sub-pipeline A, then through its Pipeline node into sub-pipeline B |
| 2 | Observe the run when sub-pipeline B's Toolkit node requires auth | "Toolkit Authorization Required" popup surfaces at the top level, with attribution correctly traceable to sub-pipeline B's Toolkit node (not misattributed to sub-pipeline A or the top-level pipeline) |
| 3 | Click **Authorize** and complete OAuth | Toolkit node's tool call executes inside sub-pipeline B |
| 4 | Observe propagation back up through the nesting levels | Sub-pipeline B completes, control returns to sub-pipeline A, which completes and returns control to the top-level pipeline, which then completes |

## Expected Final State

Two levels of pipeline nesting preserve correct authorization attribution down to the exact Toolkit node, and successful authorization correctly propagates completion back up through both nesting levels.

## Pass/Fail Criteria

**Pass:**
- Popup attribution correctly identifies the deepest nested Toolkit node despite two levels of nesting
- All nesting levels correctly resume and complete after authorization

**Fail:**
- Popup is misattributed to the wrong nesting level (e.g. shown as sub-pipeline A's own node)
- One or more nesting levels fail to resume/complete after the nested authorization is resolved
