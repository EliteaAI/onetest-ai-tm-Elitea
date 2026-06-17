---
id: ELITEA-0884
title: "Schedule Trigger — Automated Execution at Scheduled Time"
priority: high
type: functional
module: entrypoint-trigger-type
status: ready
execution_type: manual
tags: [execution, schedule, pipeline, R-2.0.3, trigger]
requirements: [#4827]
---
# ELITEA-0884: Schedule Trigger — Automated Execution at Scheduled Time

**Module:** Entrypoint Trigger Type · **Priority:** High · **Type:** Functional

**Objective:** Verifies that a pipeline with a Schedule trigger fires at the correct scheduled time, that the Entrypoint node's variables are used as pipeline input, and that the scheduled run appears in run history with a Schedule trigger notification.

## Preconditions

User is logged in
A pipeline with a Schedule trigger is configured and saved
The pipeline has at least one variable configured on the Entrypoint node for use as input
Tester has the ability to set a cron that fires within ~1-2 minutes for smoke testing

## Test Data

Cron (smoke test): */1 * * * * (every minute) — disable or change after test
Entrypoint variable: user_query = "scheduled test input"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the pipeline in edit mode and set the Schedule trigger with cron '*/1 * * * *' | Schedule is saved |
| 2 | Save the pipeline and ensure it is active | Pipeline is saved in active state |
| 3 | Wait for the next scheduled minute to pass (observe clock) | Pipeline execution starts automatically without any user input |
| 4 | Navigate to the pipeline run history | A new run entry appears in run history |
| 5 | Confirm the run completed successfully | Run status shows 'Completed' or equivalent success status |
| 6 | Inspect the run's input | Pipeline input reflects the variables configured in the Entrypoint node |
| 7 | Observe the run history entry for the scheduled run | The run entry displays a Schedule trigger notification/label, visually distinct from regular chat runs |

## Expected Final State

The run entry displays a Schedule trigger notification/label, visually distinct from regular chat runs

## Pass/Fail Criteria

PASS: Automated execution occurs at scheduled time; input = Entrypoint variables; run completes successfully; Schedule label visible in run history
FAIL: Pipeline does not fire at scheduled time; wrong input used; execution fails; no Schedule label in run history
