---
id: ELITEA-4393
title: "Re-validate: Nested Subagent/Subpipeline Runs Still Add Only +2 Messages to Context (ELITEA-0527)"
priority: critical
type: regression
module: context-management
status: draft
execution_type: manual
tags: [feat:chat, feat:context-management, feat:pipelines, issue:4840, r-2.0.8]
requirements: [EliteaAI/elitea_issues#4840]
---
# ELITEA-4393: Re-validate: Nested Subagent/Subpipeline Runs Still Add Only +2 Messages to Context (ELITEA-0527)

**Module:** Context Management · **Priority:** Critical · **Type:** Regression

**Objective:** Re-validate existing coverage for nested subagent/subpipeline message-count inflation (ELITEA-0527), since the fix for issue #4840 touches the same message-counting logic implicated in the "+4 messages" defect.

## Preconditions

- Logged in to {{base_url}}
- Existing test case ELITEA-0527 setup is available: a parent agent configured to call 1 or more nested subagents/subpipelines

## Test Data

| # | Scenario | Setup | Expected message delta |
|---|---|---|---|
| 1 | 1 nested subagent | Parent agent calls 1 subagent | +2 |
| 2 | 2 nested subagents | Parent agent calls 2 subagents | +2 |
| 3 | 1 nested subpipeline | Parent agent calls 1 subpipeline | +2 |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Execute ELITEA-0527 in full against the post-fix (R-2.0.8) build. | All steps of ELITEA-0527 complete without new failures introduced by the #4840 fix. |
| 2 | For each scenario (1 nested subagent, 2 nested subagents, 1 nested subpipeline), confirm the message delta remains exactly +2 per parent run. | Message count delta is exactly +2 for every scenario, regardless of nested call count. |
| 3 | Confirm token count delta is not multiplied by the number of nested calls. | Token count increase is proportional to actual response content, not multiplied by nested subagent/subpipeline count. |
| 4 | Record any deviation from the previously passing baseline. | No deviation from ELITEA-0527's previously passing baseline is observed. |

## Expected Final State

Nested subagent/subpipeline runs continue to add exactly +2 messages to context regardless of the number of nested calls, and token count is not multiplied by nested call count — consistent with the pre-fix passing baseline of ELITEA-0527.

## Pass/Fail Criteria

**Pass:**
- Message delta is exactly +2 for every tested scenario (1 subagent, 2 subagents, 1 subpipeline).
- Token count is not multiplied by the number of nested calls.
- No regression from the previously passing ELITEA-0527 baseline.

**Fail:**
- Message delta exceeds +2 for any scenario (e.g., +4 when 2 subagents run).
- Token count is inflated/multiplied by nested call count.
- Any previously passing ELITEA-0527 assertion now fails.
