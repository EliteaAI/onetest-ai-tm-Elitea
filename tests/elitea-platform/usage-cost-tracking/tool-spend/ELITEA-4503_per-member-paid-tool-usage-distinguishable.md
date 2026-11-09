---
id: ELITEA-4503
title: "Per-member paid-tool usage is distinguishable within a team project"
priority: high
type: functional
module: usage-cost-tracking
status: draft
execution_type: manual
tags: [feat:admin-platform, feat:chat, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6980]
---
# ELITEA-4503: Per-member paid-tool usage is distinguishable within a team project

**Module:** Usage Cost Tracking · **Priority:** High · **Type:** Functional

**Objective:** Confirm that when multiple members of a team project use a paid tool, their individual contribution to spend can be distinguished via available UI (Usage page "Whole project" vs. "My usage" views, or equivalent), consistent with how the existing LLM member budgets are shown.

**Coverage:**
- Project-level total correctly sums both members' usage
- Per-member view (if present) correctly isolates each member's own usage

## Preconditions

- A team project with at least two members, both able to trigger the paid tool

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/settings/usage` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As Member A, trigger several paid-tool calls in the team project. | Calls succeed. |
| 2 | As Member B, trigger a different number of paid-tool calls in the same team project. | Calls succeed. |
| 3 | Open Settings → Usage as an authorized user viewing "Whole project". | Paid Tools section reflects the combined project-level total (sum of both members). |
| 4 | Switch to "My usage" as Member A, then as Member B (if the paid-tool breakdown is exposed per-user). | Each member sees only their own contribution, if such a per-member paid-tool view exists. |
| 5 | If no per-member paid-tool breakdown is visible. | Note as a gap (explicitly in scope for TS3, not TS0), not a failure. |

## Expected Final State

Project-level Paid Tools total reflects combined member usage; per-member breakdown, if present, correctly isolates each member's contribution.

## Pass/Fail Criteria

**Pass:**
- Project-level total correctly sums both members' usage
- Per-member view (if present) correctly isolates each member's own usage

**Fail:**
- Project-level total is incorrect, or a per-member view (if present) shows incorrect/mixed data
