---
id: ELITEA-0873
title: "Run History — Trigger Notifications for Schedule and Webhook Runs"
priority: high
type: functional
module: entrypoint-trigger-type
status: ready
execution_type: manual
tags: [run-history, pipeline, R-2.0.3, trigger]
requirements: [#4827]
---
# ELITEA-0873: Run History — Trigger Notifications for Schedule and Webhook Runs

**Module:** Entrypoint Trigger Type · **Priority:** High · **Type:** Functional

**Objective:** Verifies that Schedule-triggered and Webhook-triggered runs each show a special trigger notification/label in pipeline run history, and that Chat Message runs show no trigger label. Also verifies the notifications are visible without opening the run detail.

## Preconditions

User is logged in
A pipeline has been run via all three trigger types: Chat Message, Schedule (using 1-min cron), and Webhook (Custom POST)
All three runs are present in pipeline run history

## Test Data

Requires three run entries: one Chat Message, one Schedule, one Webhook

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the pipeline run history | List of runs is displayed |
| 2 | Identify the run triggered via Chat Message | The run entry has no trigger notification, badge, or label |
| 3 | Identify the run triggered via Schedule | The run entry shows a visible Schedule trigger notification/label in the first message block e.g: [Scheduled execution triggered] |
| 4 | Identify the run triggered via Webhook | The run entry shows a visible Webhook trigger notification/label in the first message block e.g:  [Webhook triggered: custom/github/gitlab] Payload: ```json { "raw_payload": "longest substring without repeating characters" } ``` |
| 5 | Compare the Schedule and Webhook trigger notifications | Schedule and Webhook trigger notifications are visually distinguishable from each other |

## Expected Final State

Schedule and Webhook trigger notifications are visually distinguishable from each other

## Pass/Fail Criteria

PASS: Chat Message run has no label; Schedule run has Schedule label visible in list; Webhook run has Webhook label visible in list; Schedule and Webhook labels are visually distinct
FAIL: Chat Message run shows a trigger label; Schedule or Webhook run missing trigger label; labels not visible in list view without opening detail; Schedule and Webhook labels are identical/indistinguishable
