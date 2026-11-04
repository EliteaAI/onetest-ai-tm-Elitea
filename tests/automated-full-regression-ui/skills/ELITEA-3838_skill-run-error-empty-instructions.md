---
id: ELITEA-3838
title: "Skill Run Error — Empty/Blank Instructions Returns 400"
priority: critical
type: regression
module: elitea-platform
status: ready
execution_type: automated
tags: [feat:skills, skill-executable, error-handling, regression, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6920]
automation_test_id: []
---
# ELITEA-3838: Skill Run Error — Empty/Blank Instructions Returns 400

**Module:** Elitea Platform · **Priority:** Critical · **Type:** Regression

**Objective:** Verify that attempting to run a skill with empty or blank instructions returns HTTP 400 with a clear error message.

**Coverage:**
- API validates skill version has non-empty instructions
- Clear error message returned for empty instructions
- Prevents execution of incomplete skill versions

## Preconditions

- Logged in to {{base_url}}
- A skill version with empty/blank instructions exists, or ability to create one
- Project has default model configured

## Test Data

- Skill: Skill version with empty instructions (instructions field is empty string or only whitespace)
- User input: "Test empty instructions"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Create or identify a skill version with empty instructions field. | Skill version with blank instructions ready. |
| 2 | Send POST request to `/elitea_core/skill_predict/prompt_lib/{project_id}/{skill_id}/{empty_version_id}` with body: `{"user_input": "Test empty instructions"}`. | API rejects the request. HTTP 400 response returned. |
| 3 | Verify error response contains clear message about empty/blank instructions. | Error message indicates instructions are empty or blank (e.g., "Skill version has empty instructions" or "Instructions cannot be blank"). |
| 4 | Verify no execution occurred (no run_id, no usage event created). | No skill execution took place. No run_id in response. |

## Expected Final State

Error message indicates instructions are empty/blank and no execution occurred.

## Pass/Fail Criteria

**Pass:**
- API returns HTTP 400
- Error message clearly states instructions are empty/blank
- No execution occurred
- No run_id or usage event created

**Fail:**
- API returns HTTP 200 or attempts execution
- Error message is unclear or missing
- Execution attempted with empty instructions
