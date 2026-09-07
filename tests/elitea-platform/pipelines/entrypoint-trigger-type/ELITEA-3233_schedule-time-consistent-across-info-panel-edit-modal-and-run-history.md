---
id: ELITEA-3233
title: "Schedule time and last-run timestamp consistent across Pipeline Information, Edit schedule modal, and Run History"
priority: medium
type: functional
module: entrypoint-trigger-type
status: draft
execution_type: manual
tags: [feat:pipelines, eng:frontend, schedule, timezone]
requirements: [EliteaAI/elitea_issues#6449]
---

# ELITEA-3233: Schedule time and last-run timestamp consistent across Pipeline Information, Edit schedule modal, and Run History

**Module:** entrypoint-trigger-type · **Priority:** medium · **Type:** functional

**Objective:** Verify that the viewer-local converted schedule time is consistent across all three surfaces where it is exposed in a pipeline: the Pipeline Information panel, the entry-point node's "Edit schedule" modal, and the Run History table's last-run date/time column — for the same viewer.

**Coverage:**
- Pipeline Information panel's Schedule/Timezone/Next run matches the time configured in the Edit schedule modal, as displayed to the same viewer
- Opening the entry-point node's "Edit schedule" modal shows the schedule (cron, and any time fields) already converted to the viewer's local timezone, consistent with the Information panel
- Run History's last-run date/time column reflects the same viewer-local timezone conversion as the other two surfaces, for the same run
- No surface shows a differently-converted (or unconverted) time relative to the other two, for the same viewer

## Preconditions

- An ELITEA account with access to a pipeline that has a Schedule-triggered entry-point node
- The pipeline has executed at least once via its schedule trigger, so Run History has at least one entry
- Viewer's browser timezone is known (e.g., Asia/Calcutta, UTC+5:30)

## Test Data

| Field | Value |
|---|---|
| Cron | `51 12 * * *` |
| Viewer's browser timezone | Asia/Calcutta (UTC+5:30) |
| Expected time shown (all 3 surfaces) | 12:51 PM, Asia/Calcutta (local) |
| Example Last run (Information panel / Run History) | 9/3/26, 2:22 PM (example instant, must match across surfaces) |
| Example Next run (Information panel) | 9/4/26, 2:21 PM |

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Open the pipeline and view the Pipeline Information panel | Note the Schedule, Timezone, Last run, and Next run values shown |
| 2 | Open the entry-point/code node and click "Edit schedule" to open the schedule settings modal | Modal opens showing the same cron/schedule configuration, with any displayed time fields expressed in the viewer's local timezone, matching the Information panel from Step 1 |
| 3 | Close the modal without making changes (Cancel) | No changes are saved; Information panel values remain unchanged from Step 1 |
| 4 | Navigate to the pipeline's Run History and locate the most recent scheduled run | The date/time shown for that run matches (i.e., is consistent with) the "Last run" value shown in the Information panel in Step 1, in the viewer's local timezone |
| 5 | Compare all three captured values (Information panel, Edit schedule modal, Run History) side by side | All three surfaces present the schedule/last-run time consistently converted to the viewer's own local timezone — no discrepancy between them |

## Expected Final State

No configuration changes are made (the modal is cancelled in Step 3). All three UI surfaces continue to display the same schedule and last-run time, each correctly converted to the viewer's local timezone.

## Pass/Fail Criteria

**Pass:**
- The schedule time shown in the Edit schedule modal matches the Pipeline Information panel, for the same viewer
- The Run History last-run timestamp matches the Information panel's "Last run" value, for the same viewer
- All three surfaces are mutually consistent with no unconverted or differently-converted value on any one of them

**Fail:**
- Any one of the three surfaces shows a time that does not match the other two after accounting for the same viewer's timezone
- The Edit schedule modal displays the raw/creator timezone instead of the viewer's local timezone
- Run History shows a last-run time inconsistent with the Information panel
