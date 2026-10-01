---
id: ELITEA-3647
title: "Evaluation Analytics Empty State Display"
priority: high
type: functional
module: evaluation-run-analytics
status: ready
execution_type: manual
tags: [feat:agent_eval, feat:analytics, eng:frontend, nfr:usability, issue:6817, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6817]
---
# ELITEA-3647: Evaluation Analytics Empty State Display

**Module:** Evaluation Run Analytics · **Priority:** High · **Type:** Functional

**Objective:** Verify appropriate empty state when evaluation run has no usage data (edge case).

## Preconditions

- Logged into {{base_url}}
- Evaluation run that completed but has minimal or no tracked usage (edge case)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Analytics for an evaluation run with no/minimal data. | Analytics page loads. |
| 2 | Check Costs tab. | Shows $0.00 or empty state message, not errors. |
| 3 | Check Tokens tab. | Shows 0 or empty state, not errors. |
| 4 | Check Tools tab. | Shows empty table or "No tools used" message. |
| 5 | Check Health tab. | Shows empty or minimal data, not errors. |
| 6 | Verify no JavaScript errors in console. | No errors logged. |

## Pass/Fail Criteria

**Pass:** Empty states displayed gracefully with no errors.
**Fail:** Errors, broken UI, or misleading data when no usage exists.
