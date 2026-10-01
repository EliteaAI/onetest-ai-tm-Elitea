---
id: ELITEA-3655
title: "Evaluation Analytics Export and UX"
priority: high
type: functional
module: evaluation-run-analytics
status: draft
execution_type: manual
tags: [feat:agent_eval, feat:analytics, eng:frontend, nfr:usability, issue:6817, r-2.0.7, regression]
requirements: [EliteaAI/elitea_issues#6817]
---
# ELITEA-3655: Evaluation Analytics Export and UX

**Module:** Evaluation Run Analytics · **Priority:** High · **Type:** Regression

**Objective:** Verify Excel export, loading states, direct URL access, and browser navigation.

## Preconditions

- Logged into {{base_url}}
- Evaluation Analytics page accessible

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Evaluation Analytics for a run with data. | Analytics loads. |
| 2 | Observe loading state during page load. | Loading indicator visible until data appears. |
| 3 | Locate and click Export/Download button. | Export dialog or download triggered. |
| 4 | Download Excel file. | File downloads successfully. |
| 5 | Open downloaded file, verify data present. | Data matches displayed analytics. |
| 6 | Copy current URL from address bar. | URL copied. |
| 7 | Open new tab and paste URL. | Analytics page loads directly with same data. |
| 8 | Click browser Back button. | Returns to previous page (Results History). |
| 9 | Navigate to Analytics for run with no/minimal data. | Analytics loads. |
| 10 | Verify empty states show gracefully (no errors). | Zero values or "No data" messages, no errors. |

## Pass/Fail Criteria

**Pass:** Export works, URL is shareable, back navigation correct, empty states handled.
**Fail:** Export fails, URL not stable, navigation broken, or errors on empty data.
