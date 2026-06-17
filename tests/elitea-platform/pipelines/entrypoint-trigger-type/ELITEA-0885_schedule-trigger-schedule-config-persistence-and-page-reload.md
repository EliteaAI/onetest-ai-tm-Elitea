---
id: ELITEA-0885
title: "Schedule Trigger — Schedule Config persistence and Page Reload"
priority: medium
type: functional
module: entrypoint-trigger-type
status: ready
execution_type: manual
tags: [persistence, schedule, pipeline, R-2.0.3, trigger]
requirements: [#4827]
---
# ELITEA-0885: Schedule Trigger — Schedule Config persistence and Page Reload

**Module:** Entrypoint Trigger Type · **Priority:** Medium · **Type:** Functional

**Objective:** Verifies that saved schedule configuration persists correctly after page reload, that the YAML contains the correct trigger block (trigger.type: schedule, trigger.cron), and that the schedule reflects the browser timezone in the trigger API response.

## Preconditions

User is logged in with pipeline edit permissions
A pipeline with an Entrypoint node is open in edit mode
Access to the pipeline's YAML view and GET trigger API endpoint

## Test Data

Cron expression: 30 9 * * 1 (Every Monday at 09:30)
API endpoint: GET .../pipeline_trigger/prompt_lib/{project_id}/pipeline/{pipeline_id}/trigger

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the pipeline in edit mode, select the Entrypoint node, set Trigger to 'Schedule' | Schedule modal opens |
| 2 | In Advanced mode, enter cron '30 9 * * 1' and click Apply | Modal closes; schedule is set |
| 3 | Save the pipeline version | Pipeline is saved |
| 4 | Reload the page and open the Entrypoint node config | Trigger is still 'Schedule'; the cron '30 9 * * 1' is still present in the schedule config |
| 5 | Call the GET trigger API for this pipeline | API returns the correct cron expression; the timezone in the response matches the browser's timezone at the time of configuration |

## Expected Final State

API returns the correct cron expression; the timezone in the response matches the browser's timezone at the time of configuration

## Pass/Fail Criteria

PASS: Schedule config present after reload; YAML has trigger.type: schedule and trigger.cron; timezone matches browser
FAIL: Config lost after reload; YAML missing trigger block or has wrong values; timezone does not match browser
