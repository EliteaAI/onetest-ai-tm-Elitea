---
id: ELITEA-4691
title: "Message and Token Count Mechanics Regression Pass Under New Available Window Calculation"
priority: medium
type: regression
module: context-management
status: draft
execution_type: manual
regression: true
tags: [feat:context-management, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6898]
---

## Preconditions

- Existing manual coverage: ELITEA-0525, ELITEA-0526, ELITEA-0527, ELITEA-0528, ELITEA-0529, ELITEA-0530, ELITEA-0531

## Test Data

| Field | Value |
|-------|-------|
| Re-tested cases | ELITEA-0525, ELITEA-0526, ELITEA-0527, ELITEA-0528, ELITEA-0529, ELITEA-0530, ELITEA-0531 |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Re-execute ELITEA-0525 (toolkit tool calls do not inflate message/token count) against the new Context management widget. | Message delta is still exactly +2 regardless of tool call count. |
| 2 | Re-execute ELITEA-0527 (nested subagent/subpipeline runs add only +2 messages) against the new widget. | The same +2 delta holds under the new widget. |
| 3 | Re-execute ELITEA-0529 (token count updates immediately after Continue press) against the new widget. | Token counts still update correctly against the new available-window denominator. |
| 4 | Re-execute ELITEA-0530 (budget updates immediately after deleting a message) and ELITEA-0531 (budget fully resets after clearing a multi-message chat) against the new widget. | Both still pass; the separate Usage totals metric is NOT expected to reset/decrease during these flows (clarify this is a different metric from the live token/message count). |
| 5 | Re-execute ELITEA-0526 (in-context budget updates after each pipeline run) and ELITEA-0528 (budget does not reset after running a pipeline via chat) against the new widget. | Both still pass; the displayed denominator/percentage is consistent with the active window mode for the pipeline's model. |

## Expected Final State

All seven existing message/token counting mechanics test cases continue to pass under the new Balanced/Full budget calculation, confirming the underlying counting logic itself is unaffected by the denominator/percentage changes.

## Pass/Fail Criteria

**Pass:**
- All seven re-executed scenarios (ELITEA-0525 through ELITEA-0531) produce the same pass outcomes as before, adjusted only for the new denominator/percentage display

**Fail:**
- Any of the seven scenarios now fails due to the new window-mode calculation (e.g., incorrect message delta, incorrect reset behavior, or incorrect denominator after a pipeline run)
