---
id: ELITEA-0872
title: "Run History — Trigger Notification Visibility Without Opening Run Detail"
priority: medium
type: functional
module: entrypoint-trigger-type
status: draft
execution_type: manual
tags: [run-history, pipeline, R-2.0.3, trigger]
requirements: [EliteaAI/elitea_issues#4827]
---
# ELITEA-0872: Run History — Trigger Notification Visibility Without Opening Run Detail

**Module:** Entrypoint Trigger Type · **Priority:** Medium · **Type:** Functional

**Objective:** Verifies that the trigger notification for Schedule and Webhook runs is visible at the information section in pipeline details page without requiring the user to open the individual run detail view.

## Preconditions

Pipeline run history contains at least one Schedule-triggered run and one Webhook-triggered run
User is on the pipeline details page

## Test Data

Existing Schedule and Webhook run entries in history

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the pipeline details page | In Information section the following details should be present  e.g Trigger: Schedule: Webhook type: Timezone: Last run: |

## Expected Final State

In Information section the following details should be present  e.g Trigger: Schedule: Webhook type: Timezone: Last run:

## Pass/Fail Criteria

PASS: Trigger labels visible in run list rows without clicking
FAIL: User must open run detail to see trigger label
