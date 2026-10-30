---
id: ELITEA-4236
title: "Skill Run Error — Non-existent Skill Returns 404"
priority: critical
type: functional
module: elitea-platform
status: ready
execution_type: manual
tags: [feat:skills, skill-executable, error-handling, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6920]
---
# ELITEA-4236: Skill Run Error — Non-existent Skill Returns 404

**Module:** Elitea Platform · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that attempting to run a non-existent skill or skill version returns HTTP 404 with appropriate error message.

**Coverage:**
- API validates skill existence before execution
- API validates version existence before execution
- Clear error message for non-existent skill/version

## Preconditions

- Logged in to {{base_url}}
- Project exists with valid project_id
- Non-existent skill_id and version_id identified (e.g., random UUIDs or deleted skill)

## Test Data

- Non-existent skill_id: `00000000-0000-0000-0000-000000000000` (or any ID that doesn't exist)
- Non-existent version_id: `99999999-9999-9999-9999-999999999999`
- Existing skill_id with non-existent version_id
- User input: "Test non-existent"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Send POST request to `/elitea_core/skill_predict/prompt_lib/{project_id}/{non_existent_skill_id}` with body: `{"user_input": "Test non-existent"}`. | API rejects the request. HTTP 404 response returned. |
| 2 | Verify error message indicates skill not found. | Error message states skill does not exist (e.g., "Skill not found" or "Skill {id} does not exist"). |
| 3 | Send POST request to `/elitea_core/skill_predict/prompt_lib/{project_id}/{existing_skill_id}/{non_existent_version_id}` with body: `{"user_input": "Test"}`. | API rejects the request. HTTP 404 response returned. |
| 4 | Verify error message indicates version not found. | Error message states version does not exist (e.g., "Skill version not found" or "Version {id} does not exist"). |
| 5 | Verify no execution occurred in both cases (no run_id, no usage events). | No skill execution took place. No run_id in responses. |

## Expected Final State

No skill execution occurred in both cases and no run_id returned.

## Pass/Fail Criteria

**Pass:**
- Non-existent skill returns HTTP 404 with clear "skill not found" message
- Non-existent version returns HTTP 404 with clear "version not found" message
- No execution occurred in either case
- No run_id or usage events created

**Fail:**
- API returns HTTP 200 or wrong error code
- Error messages are unclear or missing
- Execution attempted with non-existent skill/version
