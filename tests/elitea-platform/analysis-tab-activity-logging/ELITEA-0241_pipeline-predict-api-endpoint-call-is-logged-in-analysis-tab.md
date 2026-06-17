---
id: ELITEA-0241
title: "Pipeline `/predict` API endpoint call is logged in Analysis tab"
priority: critical
type: functional
module: analysis-tab-activity-logging
status: ready
execution_type: manual
tags: [feat:analytics, issue:4007, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#4007]
---
# ELITEA-0241: Pipeline `/predict` API endpoint call is logged in Analysis tab

**Module:** Analysis Tab Activity Logging · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that a direct API call to execute a Pipeline via the predict endpoint is captured and visible in the Analysis tab.

**Coverage:**
- POST to the Pipeline predict endpoint produces a log entry in Analysis tab
- Entry is associated with the correct pipeline version and project
- API-sourced pipeline executions are not silently dropped from the log

## Preconditions

- Logged in to {{base_url}} with Editor or Admin role
- A published Pipeline exists in the current project with known `project_id` and `version_id`
- Valid Bearer API token obtained from Platform Settings → API Keys
- HTTP client available (Postman, curl, or equivalent)

## Test Data

- Base URL: `{{base_url}}`
- Endpoint: `POST /api/v2/elitea_core/predict/prompt_lib/{project_id}/{version_id}` (using Pipeline version IDs)
- Payload: `{"user_input": "Analysis tab logging test — pipeline API call"}`
- Header: `Authorization: Bearer {token}`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the Pipelines page. Open the target Pipeline. Note the `project_id` and `version_id` from the page URL or API panel. | Both IDs are recorded. |
| 2 | Send POST to the Pipeline predict endpoint with Bearer token and payload `{"user_input": "Analysis tab logging test — pipeline API call"}`. | HTTP 200 response received. Pipeline output returned in response body. |
| 3 | Navigate to the Analysis tab from the Platform sidebar. | Analysis tab opens showing activity log. |
| 4 | Locate the entry for the API pipeline call (by timestamp or pipeline name). | Entry is present — not absent. |
| 5 | Inspect the entry: verify pipeline name/version, timestamp, and project association. | Correct pipeline name/version shown, timestamp within 60 seconds of the API call, associated with correct project. |

## Expected Final State

Correct pipeline name/version shown, timestamp within 60 seconds of the API call, associated with correct project.

## Pass/Fail Criteria

**Pass:**
- Pipeline API call entry appears in Analysis tab
- Entry metadata correctly identifies the pipeline version and project

**Fail:**
- No entry in Analysis tab for the pipeline API call
- Only UI-triggered pipeline runs appear in the log
