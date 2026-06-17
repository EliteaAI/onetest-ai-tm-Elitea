---
id: ELITEA-0875
title: "YAML Persistence — Schedule and Webhook Exclusion"
priority: high
type: functional
module: entrypoint-trigger-type
status: ready
execution_type: manual
tags: [persistence, pipeline, R-2.0.3, trigger, yaml]
requirements: [#4827]
---
# ELITEA-0875: YAML Persistence — Schedule and Webhook Exclusion

**Module:** Entrypoint Trigger Type · **Priority:** High · **Type:** Functional

**Objective:** Verifies that Schedule and Webhook config is never written to YAML, that Chat Message produces no trigger block in YAML.

## Preconditions

User is logged in with pipeline edit permissions
A pipeline with an Entrypoint node is accessible with YAML view
Access to the pipeline YAML editor or view

## Test Data

Schedule cron to test: 15 7 * * 3
API endpoint: GET .../pipeline_trigger/prompt_lib/{project_id}/pipeline/{pipeline_id}/trigger

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Set Trigger to 'Schedule' with cron '15 7 * * 3' and click apply | Pipeline saves |
| 2 | Open the YAML view for the pipeline | No trigger or cron-job related fields appear in YAML |
| 3 | Switch Trigger to 'Chat Message' and save | Pipeline saves |
| 4 | Open the YAML view again | No trigger block present in YAML (or the trigger is absent / shows Chat Message marker only) |
| 5 | Set Trigger to 'Webhook' (Custom type — note the auto-generated secret displayed; do not enter a manual value) and save | Pipeline saves |
| 6 | Open the YAML view | No webhook-related fields appear in YAML |

## Expected Final State

No webhook-related fields appear in YAML

## Pass/Fail Criteria

PASS: YAML block should be unaffected by the trigger field's config; Chat Message YAML clean; Webhook YAML clean; no stale trigger blocks after type switch
FAIL: Schedule field in YAML; Chat Message has unexpected trigger block; Webhook fields in YAML;
