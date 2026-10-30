---
id: ELITEA-4230
title: "Skill Run API — Execute Default Version and Return run_id"
priority: critical
type: functional
module: elitea-platform
status: ready
execution_type: manual
tags: [feat:skills, skill-executable, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6920]
---
# ELITEA-4230: Skill Run API — Execute Default Version and Return run_id

**Module:** Elitea Platform · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that `POST /skill_predict/{project_id}/{skill_id}` executes the skill's default version and returns a response with a unique platform run_id.

**Coverage:**
- API executes skill's default version when version_id is not specified
- Response contains a unique run_id
- Skill execution completes successfully with model response

## Preconditions

- Logged in to {{base_url}}
- A skill with saved default version exists in the project
- Skill has valid non-empty instructions
- Project has default model configured

## Test Data

- Skill: Own project skill with default version set
- User input: "Hello, test the skill execution"
- Expected: Successful execution with run_id in response

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Send POST request to `/elitea_core/skill_predict/prompt_lib/{project_id}/{skill_id}` with body: `{"user_input": "Hello, test the skill execution"}` | API accepts the request. HTTP 200 response returned. |
| 2 | Verify response structure contains `run_id` field. | Response includes unique `run_id` (platform run identifier). |
| 3 | Verify response contains model's answer to the user input. | Response includes the skill's model response based on skill instructions. |
| 4 | Verify the default version was executed (check response meta or logs). | Skill's default version was used for execution. |

## Expected Final State

Response includes unique `run_id` and skill's model response based on default version instructions.

## Pass/Fail Criteria

**Pass:**
- API returns HTTP 200
- Response contains unique `run_id`
- Response contains model's answer
- Default version was executed

**Fail:**
- API returns error status
- No `run_id` in response
- Execution uses wrong version
- No model response returned
