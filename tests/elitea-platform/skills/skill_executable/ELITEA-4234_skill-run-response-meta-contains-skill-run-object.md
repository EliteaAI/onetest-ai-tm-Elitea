---
id: ELITEA-4234
title: "Skill Run Response — meta.skill_run Object Present"
priority: critical
type: functional
module: elitea-platform
status: ready
execution_type: manual
tags: [feat:skills, skill-executable, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6920]
---
# ELITEA-4234: Skill Run Response — meta.skill_run Object Present

**Module:** Elitea Platform · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that skill run response message meta contains skill_run object with skill_id, skill_version_id, and version_name.

**Coverage:**
- Response message meta includes skill_run object
- skill_run contains skill_id, skill_version_id, version_name
- Data accurate for UI rendering and history

## Preconditions

- Logged in to {{base_url}}
- A skill with saved version exists in the project
- Skill version has a name (e.g., "v1.0")
- Project has default model configured

## Test Data

- Skill: Own project skill with known skill_id, version_id, and version_name
- User input: "Test metadata"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Note the skill_id, skill_version_id, and version_name before execution. | IDs and name recorded for verification. |
| 2 | Send POST request to `/elitea_core/skill_predict/prompt_lib/{project_id}/{skill_id}` with body: `{"user_input": "Test metadata"}`. | API returns HTTP 200 with response. |
| 3 | Inspect response structure for `meta` or `message.meta` field. | Response contains meta field. |
| 4 | Verify `meta.skill_run` object exists. | skill_run object is present in meta. |
| 5 | Verify `meta.skill_run.skill_id` matches the skill used. | skill_id field matches the executed skill's ID. |
| 6 | Verify `meta.skill_run.skill_version_id` matches the version executed. | skill_version_id field matches the executed version's ID. |
| 7 | Verify `meta.skill_run.version_name` matches the version's name. | version_name field matches the version's display name (e.g., "v1.0"). |

## Expected Final State

version_name field matches the version's display name.

## Pass/Fail Criteria

**Pass:**
- Response contains meta.skill_run object
- skill_id matches executed skill
- skill_version_id matches executed version
- version_name is correct and not empty

**Fail:**
- No meta.skill_run object in response
- Any field (skill_id, skill_version_id, version_name) missing or incorrect
