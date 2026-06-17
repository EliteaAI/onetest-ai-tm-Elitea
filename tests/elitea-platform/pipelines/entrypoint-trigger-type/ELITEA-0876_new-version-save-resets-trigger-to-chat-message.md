---
id: ELITEA-0876
title: "New Version Save Resets Trigger to Chat Message"
priority: high
type: functional
module: entrypoint-trigger-type
status: draft
execution_type: manual
tags: [versioning, pipeline, R-2.0.3, trigger]
requirements: [#4827, #4975]
---
# ELITEA-0876: New Version Save Resets Trigger to Chat Message

**Module:** Entrypoint Trigger Type · **Priority:** High · **Type:** Functional

**Objective:** Verifies that saving a pipeline as a new version resets the trigger type to Chat Message on the new version (expected behavior by design), that the Webhook URL updates to reflect the new version ID, and that the user can successfully re-configure a non-Chat-Message trigger on the new version.

## Preconditions

User is logged in with pipeline edit permissions
A pipeline is configured with a Schedule or Webhook trigger and has been saved
The pipeline has a known version ID

## Test Data

Initial trigger: Schedule with cron 0 9 * * 5
Target: Save as a new version

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the pipeline configured with a Schedule trigger | Entrypoint node shows Trigger = 'Schedule' with configured cron |
| 2 | Save the pipeline as a new version (use 'Save as new version' or equivalent action) | New version is created |
| 3 | Inspect the Entrypoint node on the newly created version | Trigger type is now 'Chat Message' — the schedule config has been reset (this is expected behavior) |
| 4 | Open the Entrypoint node and set Trigger to 'Schedule', configure a new cron, and save | New trigger is saved successfully on the new version |
| 5 | Repeat steps 1-3 using a Webhook trigger (configure Webhook on an existing version, save as new version) | New version shows Trigger = 'Chat Message'; webhook config is reset |
| 6 | On the new version, configure a Webhook trigger and save | Webhook is saved successfully; the Webhook URL now reflects the new version's version_id |

## Expected Final State

Webhook is saved successfully; the Webhook URL now reflects the new version's version_id

## Pass/Fail Criteria

PASS: New version shows Chat Message after save; old trigger config not carried over; new trigger can be set successfully; webhook URL contains new version ID
FAIL: Old trigger type/config is carried over to new version unexpectedly; re-configuration fails on new version; webhook URL retains old version ID
