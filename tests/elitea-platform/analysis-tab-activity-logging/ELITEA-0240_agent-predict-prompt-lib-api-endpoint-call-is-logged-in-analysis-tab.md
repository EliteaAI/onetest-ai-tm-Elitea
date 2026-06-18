---
id: ELITEA-0240
title: "Agent `/predict/prompt_lib` API endpoint call is logged in Analysis tab"
priority: critical
type: functional
module: analysis-tab-activity-logging
status: ready
execution_type: manual
tags: [feat:analytics, issue:4007, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#4007]
---
# ELITEA-0240: Agent `/predict/prompt_lib` API endpoint call is logged in Analysis tab

**Module:** Analysis Tab Activity Logging · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that a direct API call to the Agent predict endpoint is captured and visible in the Analysis tab — this is the core regression described in the bug.

**Coverage:**
- POST to `{base_url}/api/v2/elitea_core/predict/prompt_lib/{project_id}/{version_id}` produces a log entry
- Log entry appears in Analysis tab with correct agent name, project, version, and timestamp
- API-originated calls appear alongside Chat-originated calls (no source filtering that suppresses them)

## Preconditions

- Logged in to {{base_url}} with Editor or Admin role
- A published Agent exists in the current project with known `project_id` and `version_id`
- Valid Bearer API token obtained from Platform Settings → API Keys
- HTTP client available (Postman, curl, or equivalent)

## Test Data

- Base URL: `{{base_url}}`
- Endpoint: `POST /api/v2/elitea_core/predict/prompt_lib/{project_id}/{version_id}`
- Payload: `{"user_input": "Analysis tab logging test — API call"}`
- Header: `Authorization: Bearer {token}`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the Agents page. Open the target Agent. Note the `project_id` and `version_id` from the page URL or API settings panel. | Both IDs are recorded and available for use in the API call. |
| 2 | Send POST `{base_url}/api/v2/elitea_core/predict/prompt_lib/{project_id}/{version_id}` with header `Authorization: Bearer {token}` and body `{"user_input": "Analysis tab logging test — API call"}`. | HTTP 200 response received. Response body contains non-empty AI-generated text. |
| 3 | Navigate to the Analysis tab from the Platform sidebar. | Analysis tab opens and displays the activity log. |
| 4 | Locate the entry for the API call just made (filter by timestamp or agent name if supported). | An entry corresponding to the API call is present — it is not absent or filtered out. |
| 5 | Inspect the entry details — verify agent name/version, timestamp, and project association. | Entry shows the correct agent name/version, timestamp within 60 seconds of the API call, and is associated with the correct project. |

## Expected Final State

Entry shows the correct agent name/version, timestamp within 60 seconds of the API call, and is associated with the correct project.

## Pass/Fail Criteria

**Pass:**
- Entry is visible in the Analysis tab after the API call
- Timestamp matches the API call time (within 60 seconds)
- Entry correctly identifies the tested Agent version and project

**Fail:**
- Analysis tab shows no new entry after the API call
- Only Chat-triggered calls appear; API calls are absent
- Entry appears but with incorrect agent/project metadata
