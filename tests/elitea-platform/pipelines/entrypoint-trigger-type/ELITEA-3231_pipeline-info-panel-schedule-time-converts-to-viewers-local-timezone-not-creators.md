---
id: ELITEA-3231
title: "Pipeline Information panel schedule time converts to viewer's local timezone, not creator's"
priority: high
type: functional
module: entrypoint-trigger-type
status: draft
execution_type: manual
tags: [feat:pipelines, eng:frontend, schedule, timezone]
requirements: [EliteaAI/elitea_issues#6449]
---

# ELITEA-3231: Pipeline Information panel schedule time converts to viewer's local timezone, not creator's

**Module:** entrypoint-trigger-type · **Priority:** high · **Type:** functional

**Objective:** Verify that when User A configures a Schedule trigger on a pipeline while in their own browser timezone, User B (a different account, in a different browser timezone) viewing the same pipeline's Information panel sees the Schedule/Timezone/Last run/Next run times converted to their own local timezone — not the raw time or timezone in which User A created the schedule.

**Coverage:**
- Pipeline Information panel "Timezone" field reflects the viewer's own browser timezone, not the creator's
- Pipeline Information panel "Schedule" (cron) display and its human-readable time are shown converted to viewer-local time
- "Last run" and "Next run" fields convert consistently for each viewer
- The same absolute scheduled instant is displayed correctly (and differently) to two viewers in different timezones

## Preconditions

- Two ELITEA accounts (User A, User B) with access to the same project/pipeline
- User A's machine/browser set to one timezone (e.g., UTC+5:30, Asia/Calcutta)
- User B's machine/browser set to a different timezone (e.g., UTC-5, America/New_York)
- A pipeline exists with an entry-point node whose trigger type is set to "Schedule"

## Test Data

| Field | User A (creator) | User B (viewer) |
|---|---|---|
| Browser timezone | Asia/Calcutta (UTC+5:30) | America/New_York (UTC-5) |
| Cron set by User A | `51 12 * * *` (12:51 PM local to A) | — |
| Expected Timezone field shown | Asia/Calcutta (local) | America/New_York (local) |
| Expected converted schedule time shown | 12:51 PM | 2:21 AM (same day, converted) |

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | As User A, open the pipeline, set the entry-point node's trigger to Schedule, configure cron `51 12 * * *`, and save | Pipeline Information panel shows Trigger: Schedule, Schedule: `51 12 * * *`, Timezone: Asia/Calcutta (local), with Last run/Next run populated |
| 2 | As User A, reload the page and reopen the pipeline | Information panel still shows the same schedule/time values as in Step 1, unchanged |
| 3 | As User B, log in on a machine/browser set to a different timezone and navigate to the same pipeline | Pipeline Information panel loads without error |
| 4 | As User B, inspect the Information panel's Timezone, Schedule, Last run, and Next run fields | Timezone field shows User B's own local timezone (not Asia/Calcutta); the displayed schedule/Last run/Next run times are converted to User B's local time, representing the same absolute instant User A configured |
| 5 | Compare the "Next run" value shown to User A (Step 1/2) against the "Next run" shown to User B (Step 4) | Both values represent the identical absolute point in time, each correctly converted and displayed in the respective viewer's local timezone |

## Expected Final State

The pipeline's Schedule trigger configuration is unchanged (still `51 12 * * *` as configured by User A). Each viewer's Pipeline Information panel independently displays Schedule/Timezone/Last run/Next run converted to their own browser's local timezone, with both representing the same underlying scheduled instant.

## Pass/Fail Criteria

**Pass:**
- User B's Timezone field shows User B's own timezone, not User A's
- User B's Schedule/Last run/Next run times are correctly converted to User B's local time
- User A's and User B's displayed "Next run" values, when converted back to a common reference, represent the same absolute instant

**Fail:**
- User B sees User A's raw creation-time timezone or unconverted time values
- Next run/Last run values differ from the correct converted instant
- Any inconsistency between what User A sees after reload and what User B sees
