---
id: ELITEA-3650
title: "Evaluation Analytics Browser Back Navigation"
priority: high
type: functional
module: evaluation-run-analytics
status: ready
execution_type: manual
tags: [feat:agent_eval, feat:analytics, eng:frontend, nfr:usability, issue:6817, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6817]
---
# ELITEA-3650: Evaluation Analytics Browser Back Navigation

**Module:** Evaluation Run Analytics · **Priority:** High · **Type:** Functional

**Objective:** Verify browser back button returns to previous page from evaluation analytics.

## Preconditions

- Logged into {{base_url}}

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Agent → Evaluation → Results History. | Results History page displayed. |
| 2 | Open Analytics for an evaluation run. | Analytics page opens. |
| 3 | Click browser Back button. | Returns to Results History page. |
| 4 | Verify Results History state is preserved. | Same position/scroll in Results History. |
| 5 | Open Analytics again. | Analytics page opens. |
| 6 | Navigate through tabs (Costs → Tokens → Tools). | Tab state changes. |
| 7 | Click browser Back button. | Returns to previous page (Results History), not previous tab. |

## Pass/Fail Criteria

**Pass:** Browser back navigates to previous page correctly.
**Fail:** Back button doesn't work, navigates wrong, or loses state.
