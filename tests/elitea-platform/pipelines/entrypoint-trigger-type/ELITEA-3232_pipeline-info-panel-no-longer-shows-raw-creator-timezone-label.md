---
id: ELITEA-3232
title: "Pipeline Information panel no longer shows raw creator timezone label — only viewer-local time"
priority: medium
type: functional
module: entrypoint-trigger-type
status: draft
execution_type: manual
tags: [feat:pipelines, eng:frontend, schedule, timezone]
requirements: [EliteaAI/elitea_issues#6449]
---

# ELITEA-3232: Pipeline Information panel no longer shows raw creator timezone label — only viewer-local time

**Module:** entrypoint-trigger-type · **Priority:** medium · **Type:** functional

**Objective:** Verify that the Pipeline Information panel's Timezone field unambiguously reflects the current viewer's own local timezone, with no leftover "Scheduled in `<creator tz>`, shown in `<viewer tz>`"-style dual-label wording or any other indication of the raw/original creator timezone.

**Coverage:**
- Timezone field displays only the viewer's own local timezone label (e.g., "Asia/Calcutta (local)"), with no reference to a different, original/creator timezone
- No dual-timezone or "converted from" wording is present anywhere in the Information panel
- "Next run" remains consistent with the single displayed Timezone value (no mismatch between the labeled timezone and the actual converted time)

## Preconditions

- An ELITEA account with access to a pipeline
- A pipeline exists with an entry-point node whose trigger type is set to "Schedule", created by a different account/timezone (or previously created in a different timezone than the current viewer's)

## Test Data

| Field | Value |
|---|---|
| Cron | `51 12 * * *` |
| Viewer's browser timezone | Asia/Calcutta (UTC+5:30) |
| Expected Timezone field text | `Asia/Calcutta (local)` |
| Not expected | Any secondary/original timezone label, e.g. "Scheduled: UTC-5, Shown: Asia/Calcutta" |

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Navigate to the pipeline's details and locate the Pipeline Information panel | Panel loads showing Trigger, Schedule, Timezone, Last run, Next run fields |
| 2 | Inspect the "Timezone" field text | Field shows only the viewer's own local timezone (e.g., "Asia/Calcutta (local)"), with no second/original timezone value or "Scheduled in / Shown in" style wording |
| 3 | Inspect the entire Information panel for any other mention of a differing timezone (tooltips, subtext, icons) | No dual-timezone indicator or raw creator-timezone text is present anywhere in the panel |
| 4 | Compare the "Next run" time against the single Timezone value shown | "Next run" time is consistent with (i.e., correctly expressed in) the displayed Timezone — no mismatch between the labeled timezone and the actual time shown |

## Expected Final State

No data is modified. The Information panel continues to display a single, unambiguous, viewer-local timezone label alongside a correctly converted schedule/Last run/Next run time.

## Pass/Fail Criteria

**Pass:**
- Only one timezone (the viewer's own local timezone) is displayed anywhere in the Information panel
- No wording implies a separate "original" or "creator" timezone
- Next run time is consistent with the single displayed timezone

**Fail:**
- Any dual-timezone label, tooltip, or wording referencing the creator's/original timezone is present
- The displayed Timezone value and the actual converted time are inconsistent with each other
