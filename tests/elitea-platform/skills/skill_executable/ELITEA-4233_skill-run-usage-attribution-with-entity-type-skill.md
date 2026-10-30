---
id: ELITEA-4233
title: "Skill Run Usage Attribution — entity_type='skill' with Correct IDs"
priority: critical
type: functional
module: elitea-platform
status: ready
execution_type: manual
tags: [feat:skills, skill-executable, usage-tracking, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6920]
---
# ELITEA-4233: Skill Run Usage Attribution — entity_type='skill' with Correct IDs

**Module:** Elitea Platform · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that skill run creates usage rows with entity_type='skill', root_entity_type='skill', and correct skill_id/version_id.

**Coverage:**
- Usage event created for skill execution
- entity_type and root_entity_type set to 'skill'
- skill_id and skill_version_id correctly recorded
- Usage tracked for billing/analytics

## Preconditions

- Logged in to {{base_url}} with access to usage database
- A skill with saved version exists in the project
- Project has default model configured
- Access to query usage_event table or Usage API

## Test Data

- Skill: Own project skill with known skill_id and version_id
- User input: "Test usage tracking"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Note the skill_id and skill_version_id before execution. | IDs recorded for verification. |
| 2 | Send POST request to `/elitea_core/skill_predict/prompt_lib/{project_id}/{skill_id}` with body: `{"user_input": "Test usage tracking"}`. | API returns HTTP 200 with run_id. |
| 3 | Query usage_event table or Usage API using the returned run_id. | Usage row(s) found for this run_id. |
| 4 | Verify usage row has `entity_type = 'skill'`. | entity_type field equals 'skill'. |
| 5 | Verify usage row has `root_entity_type = 'skill'`. | root_entity_type field equals 'skill'. |
| 6 | Verify usage row contains correct `skill_id` (entity_id field). | entity_id matches the skill_id used in API call. |
| 7 | Verify usage row contains correct `skill_version_id` (version_id field). | version_id matches the skill_version_id executed. |

## Expected Final State

entity_id matches the skill_id used in API call and version_id matches the executed skill_version_id.

## Pass/Fail Criteria

**Pass:**
- Usage row(s) created for the run
- entity_type = 'skill'
- root_entity_type = 'skill'
- entity_id matches skill_id
- version_id matches skill_version_id

**Fail:**
- No usage row created
- entity_type or root_entity_type is not 'skill'
- Incorrect skill_id or version_id in usage row
