---
id: ELITEA-0871
title: "Migration — Existing Pipelines Auto-Assigned Chat Message Trigger"
priority: high
type: functional
module: entrypoint-trigger-type
status: ready
execution_type: manual
tags: [regression, migration, pipeline, R-2.0.3, trigger]
requirements: [EliteaAI/elitea_issues#4827]
---
# ELITEA-0871: Migration — Existing Pipelines Auto-Assigned Chat Message Trigger

**Module:** Entrypoint Trigger Type · **Priority:** High · **Type:** Functional

**Objective:** Verifies that all pre-existing pipelines are automatically assigned the Chat Message trigger after the R-2.0.3 deployment, that migrated pipelines execute correctly from chat without any reconfiguration, and that pipelines without an Entrypoint node are unaffected.

## Preconditions

The R-2.0.3 deployment has been applied
Pre-existing pipelines were created before the deployment (at least two: one with an Entrypoint node, one without)
The pre-existing pipeline with an Entrypoint node was working correctly before deployment

## Test Data

Pipeline A: pre-existing, has Entrypoint node — should show Chat Message trigger post-migration
Pipeline B: pre-existing, has NO Entrypoint node — should be unaffected
Chat message to test execution: "migration test input"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | After deployment, open Pipeline A (pre-existing, has Entrypoint node) in edit mode | Pipeline opens successfully |
| 2 | Inspect the Entrypoint node's Trigger field | Trigger type is 'Chat Message' — automatically assigned by migration |
| 3 | Execute Pipeline A by sending a chat message | Pipeline executes successfully end-to-end with no manual reconfiguration needed |
| 4 | Confirm execution results match pre-migration behavior | Pipeline output is correct and consistent with pre-migration runs |
| 5 | Open Pipeline B (pre-existing, has NO Entrypoint node) in edit mode | Pipeline opens successfully; no Entrypoint node is marked |
| 6 | Inspect Pipeline B's configuration | Pipeline B is unaffected — no trigger field has been added to non-Entrypoint nodes; pipeline is in the same state as pre-migration |
| 7 | Check all other pre-existing pipelines with Entrypoint nodes (spot-check) | Each one shows Chat Message as the trigger type |

## Expected Final State

Each one shows Chat Message as the trigger type

## Pass/Fail Criteria

PASS: All pre-existing pipelines with Entrypoint -> Chat Message trigger; execute correctly from chat; pipelines without Entrypoint unaffected
FAIL: Any pre-existing pipeline with Entrypoint shows a different trigger type; execution fails post-migration; pipelines without Entrypoint are broken or modified
