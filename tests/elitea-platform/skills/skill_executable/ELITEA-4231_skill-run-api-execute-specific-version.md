---
id: ELITEA-4231
title: "Skill Run API — Execute Specific Version"
priority: critical
type: functional
module: elitea-platform
status: ready
execution_type: manual
tags: [feat:skills, skill-executable, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6920]
---
# ELITEA-4231: Skill Run API — Execute Specific Version

**Module:** Elitea Platform · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that `POST /skill_predict/{project_id}/{skill_id}/{version_id}` executes the specified version of the skill.

**Coverage:**
- API executes exact version specified in the endpoint
- Different version instructions result in different responses
- Version selection is accurate

## Preconditions

- Logged in to {{base_url}}
- A skill with multiple saved versions exists in the project
- Each version has distinct instructions (e.g., v1: "Be formal", v2: "Be casual")
- Project has default model configured

## Test Data

- Skill: Own project skill with at least 2 versions
- Version 1 ID: `{version_id_1}` with distinct instructions
- Version 2 ID: `{version_id_2}` with different instructions
- User input: "Explain what you do"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Send POST request to `/elitea_core/skill_predict/prompt_lib/{project_id}/{skill_id}/{version_id_1}` with body: `{"user_input": "Explain what you do"}` | API accepts the request. HTTP 200 response returned. |
| 2 | Verify response reflects version 1's instructions (e.g., formal tone if v1 is formal). | Response follows version 1's specific instruction style. |
| 3 | Send POST request to `/elitea_core/skill_predict/prompt_lib/{project_id}/{skill_id}/{version_id_2}` with same user input. | API accepts the request. HTTP 200 response returned. |
| 4 | Verify response reflects version 2's instructions (e.g., casual tone if v2 is casual). | Response follows version 2's specific instruction style, different from version 1. |
| 5 | Compare both responses to confirm they differ according to their version instructions. | Responses are distinctly different, confirming correct version execution. |

## Expected Final State

Responses are distinctly different, confirming correct version execution.

## Pass/Fail Criteria

**Pass:**
- Both API calls return HTTP 200
- Response from version 1 follows version 1 instructions
- Response from version 2 follows version 2 instructions
- Responses are clearly different based on version instructions

**Fail:**
- API returns error status
- Both versions produce identical responses
- Response doesn't match specified version's instructions
