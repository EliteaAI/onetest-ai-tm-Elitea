---
id: ELITEA-3608
title: "Pipeline Run Analytics Opens from Context Menu"
priority: critical
type: functional
module: per-run-analytics
status: ready
execution_type: manual
tags: [feat:analytics, feat:pipelines, eng:frontend, issue:6816, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6816]
---
# ELITEA-3608: Pipeline Run Analytics Opens from Context Menu

**Module:** Per-Run Analytics · **Priority:** Critical · **Type:** Functional

**Objective:** Verify clicking "Analytics" in Pipeline Run History opens Per-Run Analytics page with correct data.

## Preconditions

- Logged into {{base_url}}
- A Pipeline with at least one prior execution exists
- Pipeline Run History panel is open

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Pipeline Run History panel. | Run History panel displays past runs. |
| 2 | Right-click on a specific run row (note the date/version). | Context menu appears. |
| 3 | Click "Analytics" option. | Per-Run Analytics page opens. |
| 4 | Verify page loads without errors. | Analytics page displays with data. |
| 5 | Verify data corresponds to selected run. | Analytics data matches the selected run (not project-wide). |

## Pass/Fail Criteria

**Pass:** Per-Run Analytics page opens with run-specific data for the pipeline.
**Fail:** Page fails to open, shows error, or displays project-wide data instead of run-specific.
