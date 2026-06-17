---
id: ELITEA-0886
title: "Schedule Trigger — Modal UI, Default and Advanced Modes, Live Summary"
priority: high
type: functional
module: entrypoint-trigger-type
status: ready
execution_type: manual
tags: [schedule, pipeline, R-2.0.3, trigger]
requirements: [#4827, #4975]
---
# ELITEA-0886: Schedule Trigger — Modal UI, Default and Advanced Modes, Live Summary

**Module:** Entrypoint Trigger Type · **Priority:** High · **Type:** Functional

**Objective:** Verifies that selecting Schedule opens the Schedule settings modal with Cancel/Apply buttons, that Default mode shows the correct fields (Every day/week/month, on day-of-week, at hour:minute), that Advanced mode shows a cron expression input, that the summary text updates live as fields are changed, and that Cancel discards changes while Apply saves them.

## Preconditions

User is logged in with pipeline edit permissions
A pipeline with an Entrypoint node is open in edit mode

## Test Data

Default mode selection: Every Week, on Saturday, at 10:00
Advanced mode cron: 0 10 * * 6
Invalid cron: 99 99 99 99 99
Empty cron: (blank field)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Click the Entrypoint node to open its config panel | Node config opens |
| 2 | Select 'Schedule' from the Trigger dropdown | A Schedule settings modal opens with Cancel and Apply buttons visible |
| 3 | Confirm the modal is in Default mode by default | Default mode is active; fields shown are: Every [day/week/month selector], on [day-of-week selector], at [hour]:[minute] |
| 4 | Set 'Every' to 'day' and observe the visible fields | Only hour and minute fields are shown — no day-of-week selector |
| 5 | Set 'Every' to 'month' and observe the visible fields | Day-of-month and time fields are shown |
| 6 | Set 'Every' to 'week', select 'Saturday' as day, set time to 10:00 | Fields accept the input |
| 7 | Observe the summary text at the top of the modal after setting 'Every week, Saturday, 10:00' | Summary text updates to reflect the selection (e.g., 'At 10:00, only on Saturday') |
| 8 | Switch to Advanced mode | A cron expression text input field is displayed; the equivalent cron string for the current Default mode selection is pre-filled (e.g., 0 10 * * 6) |
| 9 | Clear the cron field and click Apply | Apply is blocked; a validation message appears indicating the cron cannot be empty |
| 10 | Enter an invalid cron string (e.g., 99 99 99 99 99) and click Apply | Apply is blocked; a validation error is displayed |
| 11 | Enter a valid cron string (e.g., 0 10 * * 6) and click Apply | Modal closes; schedule is saved; the Entrypoint node shows the configured schedule |
| 12 | Re-open the Schedule modal and click Cancel without making changes | Modal closes; previously saved schedule remains unchanged |
| 13 | Re-open the Schedule modal, change the cron to something different, then click Cancel | Modal closes; the previous cron value is preserved — changes are discarded |

## Expected Final State

Modal closes; the previous cron value is preserved — changes are discarded

## Pass/Fail Criteria

PASS: Modal opens on Schedule selection; Cancel/Apply present; Default and Advanced modes function correctly; summary updates live; invalid/empty cron blocked; Cancel discards; Apply saves
FAIL: Modal does not open; Cancel/Apply absent; summary does not update; invalid cron accepted; Cancel saves changes unexpectedly
