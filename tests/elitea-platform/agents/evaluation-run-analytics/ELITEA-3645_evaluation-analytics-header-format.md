---
id: ELITEA-3645
title: "Evaluation Analytics Header Format with Suite Name"
priority: critical
type: functional
module: evaluation-run-analytics
status: ready
execution_type: manual
tags: [feat:agent_eval, feat:analytics, eng:frontend, issue:6817, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6817]
---
# ELITEA-3645: Evaluation Analytics Header Format with Suite Name

**Module:** Evaluation Run Analytics · **Priority:** Critical · **Type:** Functional

**Objective:** Verify header displays correct format with date, suite name, and evaluated agent version.

## Preconditions

- Logged into {{base_url}}
- Evaluation Analytics page open
- Evaluation run has known suite name and version

## Test Data

- Evaluation run: "02 Sep 2026, 12:23 PM", Suite: "Regression Suite", Version: "v2"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Evaluation Analytics for an evaluation run. | Analytics page loads. |
| 2 | Locate the header section below breadcrumb. | Header section visible. |
| 3 | Verify header format. | Shows: "Run: DD MMM YYYY, HH:MM AM/PM · Suite: [suite_name] · Version: [version]" |
| 4 | Verify date matches the selected evaluation's execution date. | Date is correct. |
| 5 | Verify Suite name is displayed. | Suite name matches the evaluation suite that was run. |
| 6 | Verify Version shows the EVALUATED agent version. | Version matches what was evaluated (not current editor version). |

## Pass/Fail Criteria

**Pass:** Header shows "Run: [date] · Suite: [suite] · Version: [version]" with correct values.
**Fail:** Header missing, wrong format, or Suite name not displayed.
