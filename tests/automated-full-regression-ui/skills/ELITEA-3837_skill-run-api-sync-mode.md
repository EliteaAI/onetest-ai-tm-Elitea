---
id: ELITEA-3837
title: "Skill Run API — Sync Mode Returns Response Successfully"
priority: critical
type: regression
module: elitea-platform
status: ready
execution_type: automated
tags: [feat:skills, skill-executable, regression, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6920]
automation_test_id: []
---
# ELITEA-3837: Skill Run API — Sync Mode Returns Response Successfully

**Module:** Elitea Platform · **Priority:** Critical · **Type:** Regression

**Objective:** Verify that sync mode (default) returns the skill response immediately without requiring async task polling.

**Coverage:**
- Sync execution completes in one request-response cycle
- No task_id or callback mechanism required
- Response delivered immediately

## Preconditions

- Logged in to {{base_url}}
- A skill with saved version exists in the project
- Project has default model configured

## Test Data

- Skill: Own project skill with valid instructions
- User input: "What is 2+2?"
- async_mode: not set (defaults to false) or explicitly set to false

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Send POST request to `/elitea_core/skill_predict/prompt_lib/{project_id}/{skill_id}` with body: `{"user_input": "What is 2+2?"}` (no async_mode or async_mode: false). | API accepts the request. |
| 2 | Wait for response (should be immediate, not delayed). | HTTP 200 response returned within reasonable time (< 30 seconds for simple query). |
| 3 | Verify response contains the model's direct answer in the response body. | Response includes model's answer (e.g., "4" or explanation). |
| 4 | Verify no `task_id` field is present in response (sync mode doesn't return task_id). | Response structure contains answer directly, no task_id field present. |
| 5 | Verify `run_id` is present in response. | Response includes unique `run_id` field. |

## Expected Final State

Response includes unique `run_id` field and model's direct answer without task_id.

## Pass/Fail Criteria

**Pass:**
- API returns HTTP 200 immediately
- Response contains model's answer in the body
- No `task_id` in response
- `run_id` is present
- Total response time < 30 seconds

**Fail:**
- API returns task_id requiring polling
- Response delayed or requires separate retrieval
- No answer in immediate response
- No `run_id` present
