---
id: ELITEA-0877
title: "Trigger Type Switching — Config Clearance and State Isolation"
priority: high
type: functional
module: entrypoint-trigger-type
status: ready
execution_type: manual
tags: [pipeline, R-2.0.3, trigger, state]
requirements: [EliteaAI/elitea_issues#4827]
---
# ELITEA-0877: Trigger Type Switching — Config Clearance and State Isolation

**Module:** Entrypoint Trigger Type · **Priority:** High · **Type:** Functional

**Objective:** Verifies that switching between trigger types (Schedule <-> Webhook <-> Chat Message) correctly clears the previous type's configuration and only shows config relevant to the newly selected type.

## Preconditions

User is logged in with pipeline edit permissions
A pipeline with an Entrypoint node is open in edit mode

## Test Data

Schedule cron: 0 8 * * 1
Webhook type: Custom (auto-generated secret — note from UI after selecting Webhook)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Set Trigger to 'Schedule', configure a cron (0 8 * * 1), and apply | Schedule config is saved on the node |
| 2 | Change Trigger from 'Schedule' to 'Webhook' | Webhook config section appears (type, URL, auto-generated secret); schedule-related fields and cron are no longer visible |
| 3 | Configure Webhook (Custom type, note the auto-generated secret), then switch Trigger from 'Webhook' to 'Schedule' | Schedule config fields appear; webhook fields (URL, secret) are no longer visible |
| 4 | Configure a schedule, then switch Trigger from 'Schedule' to 'Chat Message' | No trigger-specific config fields are shown; the section below the dropdown is empty |
| 5 | Switch from 'Webhook' (configured) to 'Chat Message' | No trigger-specific config fields remain; webhook fields are removed |

## Expected Final State

No trigger-specific config fields remain; webhook fields are removed

## Pass/Fail Criteria

PASS: Switching types clears previous config; correct fields shown for new type; Chat Message shows no config
FAIL: Previous type's config persists after switching; wrong fields shown; stale config retained in UI
