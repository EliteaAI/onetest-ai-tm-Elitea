---
id: ELITEA-3625
title: "E2E Pipeline Per-Run Analytics Flow"
priority: critical
type: e2e
module: per-run-analytics
status: draft
execution_type: automated
tags: [feat:analytics, feat:pipelines, eng:frontend, issue:6816, r-2.0.7, regression]
requirements: [EliteaAI/elitea_issues#6816]
---
# ELITEA-3625: E2E Pipeline Per-Run Analytics Flow

**Module:** Per-Run Analytics · **Priority:** Critical · **Type:** E2E Regression

**Objective:** End-to-end verification of Per-Run Analytics for Pipelines: navigation, UI structure, and data display.

## Preconditions

- Logged into {{base_url}}
- Pipeline with prior runs exists
- Test data: Pipeline "Regression Test Pipeline" with runs including tool usage

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Pipelines page. | Pipelines list loads. |
| 2 | Open "Regression Test Pipeline". | Pipeline detail page opens. |
| 3 | Click history icon to open Run History panel. | Panel opens with run list. |
| 4 | Right-click on most recent run row. | Context menu appears. |
| 5 | Verify "Analytics" option present. | Option visible (same position as Agents). |
| 6 | Click "Analytics" option. | Per-Run Analytics page opens. |
| 7 | Verify breadcrumb: `Pipelines / [Name] / Run History / Analytics`. | Breadcrumb correct. |
| 8 | Verify header format matches Agent format. | "Run: [date] · Version: [version]". |
| 9 | Verify same 4 tabs as Agent analytics. | Costs, Tokens, Tools, Health. |
| 10 | Click through all tabs. | Each tab loads without errors. |
| 11 | Verify data is run-scoped (not project-wide). | Values appropriate for single run. |
| 12 | Click Export button. | Export completes successfully. |
| 13 | Click breadcrumb "Pipelines" segment. | Navigates to Pipelines list. |

## Automation Notes

- Reuse Agent test selectors where applicable
- Verify UI consistency between Agent and Pipeline analytics

## Pass/Fail Criteria

**Pass:** Pipeline analytics works identically to Agent analytics.
**Fail:** Any difference in behavior or missing functionality.
