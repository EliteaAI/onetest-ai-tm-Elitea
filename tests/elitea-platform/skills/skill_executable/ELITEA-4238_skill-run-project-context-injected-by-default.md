---
id: ELITEA-4238
title: "Skill Run Configuration — Project Context Injected by Default"
priority: critical
type: functional
module: elitea-platform
status: ready
execution_type: manual
tags: [feat:skills, skill-executable, configuration, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6920]
---
# ELITEA-4238: Skill Run Configuration — Project Context Injected by Default

**Module:** Elitea Platform · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that project context is injected into the system prompt by default when executing a skill.

**Coverage:**
- Project context automatically included in skill execution
- Skill can access project-specific information
- Default behavior includes project context

## Preconditions

- Logged in to {{base_url}}
- A skill with saved version exists in the project
- Project has project context configured (e.g., project description, guidelines, or indexed data)
- Project context contains identifiable information

## Test Data

- Skill: Own project skill with instructions like "Answer questions about this project"
- Project context: Contains specific project information (e.g., "Project XYZ is a customer support automation system")
- User input: "What is this project about?"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Verify project has context configured in Project Settings. | Project context exists and contains identifiable information. |
| 2 | Send POST request to `/elitea_core/skill_predict/prompt_lib/{project_id}/{skill_id}` with body: `{"user_input": "What is this project about?"}` (no special flags). | API returns HTTP 200 with response. |
| 3 | Verify model response references information from project context. | Response includes details from project context (e.g., mentions "customer support automation" or project-specific info). |
| 4 | Verify model can answer project-specific questions it wouldn't know without context. | Model demonstrates knowledge of project context that wasn't in the skill instructions alone. |

## Expected Final State

Model demonstrates knowledge of project context in its response.

## Pass/Fail Criteria

**Pass:**
- Model response references project context information
- Model can answer project-specific questions
- Project context was injected by default (no flag required)

**Fail:**
- Model cannot access project context
- Model responds with generic information only
- Model states it doesn't have project information
