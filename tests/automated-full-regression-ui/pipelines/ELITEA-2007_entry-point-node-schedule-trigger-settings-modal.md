---
id: ELITEA-2007
title: "Pipeline Editor — Schedule Settings on the New Schedule Page"
priority: medium
type: functional
module: pipelines
status: ready
execution_type: automated
automation_test_id:
  - tests.ui.pipelines_2.test_pipeline_schedule_trigger_settings_modal.test_schedule_trigger_settings_modal
automation_pr: https://github.com/EliteaAI/elitea-testing-public/commit/1e43c0d2
tags: [automated:UI:regression, feat:pipelines]
requirements: []
---

# ELITEA-2007: Pipeline Editor — Schedule Settings on the New Schedule Page

**Module:** pipelines · **Priority:** medium · **Type:** functional

**Objective:** Verify that a schedule created from the SCHEDULES section of the pipeline editor ("+ Schedule" → New Schedule page) offers Builder and Cron Expression modes with correct controls, that the summary updates dynamically, and that the schedule persists after save and reload. (Schedule is no longer a Trigger option — EliteaAI/elitea_issues#7011, #7338.)

---

## Preconditions

- User is logged in to the Elitea platform.
- A pipeline exists with an entry point node and no HITL/Printer/interrupts.

---

## Test Data

| Field | Value |
|-------|-------|
| Hour | 09 |
| Minute | 30 |
| Name | any unique name |
| Expected summary (daily) | Runs every day at 09:30. |
| Expected card rule | At 09:30 |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open a pipeline with an entry point node and no HITL/Printer/interrupts; in the left panel find the SCHEDULES section and click "+ Schedule" | SCHEDULES section shows "No schedules run the base version yet."; the New Schedule page opens |
| 2 | Check "What to Run" | Pipeline is pre-filled and locked to this pipeline; Version is pre-selected (leave as is) |
| 3 | Fill Name (required); in SCHEDULE SETTINGS stay on the Builder tab | Fields Every / on / at and the summary line are shown |
| 4 | Change "Every" to "day" | The "on" field is hidden |
| 5 | Set the time to 09:30 | Summary updates to "Runs every day at 09:30." |
| 6 | Switch to the Cron Expression tab | The cron input is shown |
| 7 | Switch back to Builder | The Every / on / at fields return |
| 8 | Click Save | Back on the pipeline, a schedule card appears in the SCHEDULES section showing the rule (every day at 09:30) |
| 9 | Reload the page | The schedule card is still there with the same rule |

---|--------|-----------------|
| 1 | Create a pipeline with entry point node, no HITL/Printer/interrupts | Pipeline is ready with a single entry point node |
| 2 | Select "Schedule" from Trigger dropdown | Trigger dropdown updates to "Schedule" |
| 3 | Verify "Schedule settings" modal opens with: Summary line, Mode radio (Default/Advanced), Default mode fields (Every dropdown, on dropdown, at hour:minute), Helper text, Cancel/Apply buttons | All listed elements are present and correctly displayed |
| 4 | Change "Every" to "day" — verify "on" field hides (not applicable for daily) | The "on" day-of-week field is hidden when "day" is selected |
| 5 | Change hour to "09", minute to "30" — verify summary updates (e.g., "At 09:30, every day") | Summary line updates dynamically to reflect the new schedule |
| 6 | Switch to "Advanced" mode — verify cron expression input appears | Cron expression text input is shown |
| 7 | Switch back to "Default" — verify dropdowns return | Default mode dropdowns are restored |
| 8 | Click "Apply" — verify modal closes, Trigger shows "Schedule" | Modal closes and entry point shows "Schedule" trigger |
| 9 | Save pipeline — reload — verify Schedule trigger persists | Schedule trigger is present after page reload |

---

## Expected Final State

The New Schedule page is fully functional: Builder and Cron Expression modes work correctly, the summary updates dynamically, and the schedule card persists after save/reload.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- All schedule form elements are present, the dynamic summary updates correctly, and the schedule card persists after reload.

**Fail:**
- Any step produces an error or unexpected result.
- Form elements are missing, the summary does not update, or the schedule does not persist.
