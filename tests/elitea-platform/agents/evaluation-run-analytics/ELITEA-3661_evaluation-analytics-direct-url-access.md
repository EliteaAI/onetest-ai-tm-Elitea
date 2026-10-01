---
id: ELITEA-3661
title: "Evaluation Analytics Direct URL Access"
priority: high
type: functional
module: evaluation-run-analytics
status: ready
execution_type: manual
tags: [feat:agent_eval, feat:analytics, eng:frontend, nfr:usability, issue:6817, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6817]
---
# ELITEA-3661: Evaluation Analytics Direct URL Access

**Module:** Evaluation Run Analytics · **Priority:** High · **Type:** Functional

**Objective:** Verify evaluation analytics page can be accessed directly via URL (bookmarkable/shareable).

## Preconditions

- Logged into {{base_url}}
- Evaluation Analytics page previously accessed

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Evaluation Analytics through normal navigation. | Analytics page opens. |
| 2 | Copy the current URL from browser address bar. | URL copied. |
| 3 | Open a new browser tab. | New tab opens. |
| 4 | Paste and navigate to the copied URL. | Analytics page loads directly. |
| 5 | Verify correct data is displayed. | Same evaluation run's analytics shown. |
| 6 | Verify breadcrumb is correct. | Breadcrumb matches the agent/suite context. |
| 7 | Share URL with another user (same permissions). | They can access the same page. |

## Pass/Fail Criteria

**Pass:** Direct URL access loads correct evaluation analytics page.
**Fail:** URL not stable, wrong data, or access denied on direct navigation.
