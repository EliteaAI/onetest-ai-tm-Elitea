---
id: ELITEA-3313
title: "Context handling in nested pipeline scenarios works correctly"
priority: medium
type: functional
module: pipelines
status: ready
execution_type: manual
tags: [feat:context-management, feat:toolkits, story:6306, r-2.0.6, sub-pipeline, nested]
requirements: [EliteaAI/elitea_issues#6306]
---

# ELITEA-3313: Context handling in nested pipeline scenarios works correctly

## Preconditions

- User is logged in to `{{base_url}}`
- A parent pipeline exists that calls a sub-pipeline
- The sub-pipeline contains Skill Builder or Project Context Builder tool
- User has access to the test project

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create a sub-pipeline that uses Skill Builder to create a skill | Sub-pipeline saved |
| 2 | Create a parent pipeline that calls the sub-pipeline | Parent pipeline saved |
| 3 | Execute the parent pipeline in Project A | Pipeline execution starts |
| 4 | Verify the skill created by the sub-pipeline is in Project A | Skill appears in Project A's Skills list |
| 5 | Fork or recreate the parent pipeline in Project B | Parent pipeline exists in Project B |
| 6 | Execute the parent pipeline in Project B | Pipeline execution starts |
| 7 | Verify the skill created by the sub-pipeline is in Project B | Skill appears in Project B's Skills list |

## Expected Final State

When Skill Builder or Project Context Builder is used within a sub-pipeline, the runtime_context correctly propagates from the parent context. Skills/Contexts are created in the correct project regardless of nesting depth.

## Pass/Fail Criteria

**Pass:**
- Sub-pipeline correctly inherits parent's project context
- Skills created in the correct project
- Nesting does not break context injection
- Same sub-pipeline works correctly in different parent projects

**Fail:**
- Sub-pipeline uses wrong project context
- Skills created in a fixed project regardless of parent
- Context lost during pipeline nesting
