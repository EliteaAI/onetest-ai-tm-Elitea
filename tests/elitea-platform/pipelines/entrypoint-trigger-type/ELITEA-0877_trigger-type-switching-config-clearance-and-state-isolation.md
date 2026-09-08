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
Pipeline does not contain OAuth-requiring toolkits (if OAuth toolkit present, Schedule/Webhook triggers cannot be selected per issue #6128)

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
| 6 | Add an OAuth-requiring toolkit (e.g., Azure SharePoint Delegated) to the pipeline with Chat Message trigger selected | OAuth toolkit added successfully |
| 7 | Attempt to switch Trigger to 'Schedule' | 'Schedule' option is disabled; cannot be selected |
| 8 | Attempt to switch Trigger to 'Webhook' | 'Webhook' option is disabled; cannot be selected |
| 9 | Verify only Chat Message trigger is available | Chat Message is the only enabled option |
| 10 | Remove OAuth toolkit from pipeline | OAuth toolkit removed |
| 11 | Verify all trigger types become available again | Schedule, Webhook, and Chat Message all enabled |

## Expected Final State

No trigger-specific config fields remain; webhook fields are removed

## Pass/Fail Criteria

PASS: Switching types clears previous config; correct fields shown for new type; Chat Message shows no config
FAIL: Previous type's config persists after switching; wrong fields shown; stale config retained in UI
