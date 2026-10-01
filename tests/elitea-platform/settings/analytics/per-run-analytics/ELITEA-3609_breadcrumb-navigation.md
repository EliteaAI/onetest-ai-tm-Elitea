---
id: ELITEA-3609
title: "Per-Run Analytics Breadcrumb Navigation"
priority: critical
type: functional
module: per-run-analytics
status: ready
execution_type: manual
tags: [feat:analytics, eng:frontend, nfr:usability, issue:6816, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6816]
---
# ELITEA-3609: Per-Run Analytics Breadcrumb Navigation

**Module:** Per-Run Analytics · **Priority:** Critical · **Type:** Functional

**Objective:** Verify breadcrumb shows correct path and each segment navigates correctly for both Agents and Pipelines.

## Preconditions

- Logged into {{base_url}}
- Per-Run Analytics page open for an Agent or Pipeline run

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Per-Run Analytics for an Agent run. | Analytics page loads. |
| 2 | Verify breadcrumb format for Agent. | Shows: `Agents / [Agent Name] / Run History / Analytics` |
| 3 | Click "Agents" segment in breadcrumb. | Navigates to Agents list page. |
| 4 | Navigate back to Analytics page. | Analytics page loads again. |
| 5 | Click "[Agent Name]" segment. | Navigates to Agent detail page. |
| 6 | Open Per-Run Analytics for a Pipeline run. | Analytics page loads. |
| 7 | Verify breadcrumb format for Pipeline. | Shows: `Pipelines / [Pipeline Name] / Run History / Analytics` |
| 8 | Click breadcrumb segments. | Each navigates to correct location. |

## Pass/Fail Criteria

**Pass:** Breadcrumb displays correct format for both Agents and Pipelines, all segments navigate correctly.
**Fail:** Breadcrumb missing, incorrect format, or navigation fails.
