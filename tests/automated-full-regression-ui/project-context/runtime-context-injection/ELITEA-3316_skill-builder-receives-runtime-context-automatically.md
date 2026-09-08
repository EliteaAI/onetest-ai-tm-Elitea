---
id: ELITEA-3316
title: "Skill Builder receives runtime_context and creates skill in current project only"
priority: critical
type: functional
module: skills
status: ready
execution_type: manual
tags: [feat:context-management, feat:toolkits, story:6306, r-2.0.6, runtime-context, skills-builder]
requirements: [EliteaAI/elitea_issues#6306]
---

# ELITEA-3316: Skill Builder receives runtime_context and creates skill in current project only

## Preconditions

- User is logged in to `{{base_url}}`
- Skills Builder module is enabled in Chat Modules
- User is in Project A (note the project name/id)
- User has access to at least one other project (Project B)

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Confirm you are in Project A by checking the project selector | Project A is selected |
| 2 | Open Chat Modules menu and enable Skills Builder | Skills Builder toggle is enabled |
| 3 | Send: "Create a skill called 'Meeting Notes Summarizer' that summarizes meeting notes into action items" | The assistant proceeds with Skill creation without asking for project specification |
| 4 | Verify the Skill chip/link appears in the chat response | Skill chip is present |
| 5 | Navigate to Project A's Skills list | The "Meeting Notes Summarizer" skill is present |
| 6 | Navigate to Project B's Skills list | The "Meeting Notes Summarizer" skill is NOT present |

## Expected Final State

Skill Builder automatically receives runtime_context containing user_id and project_id, creating the skill in the correct project without requiring explicit user input. The skill is isolated to the current project only.

## Pass/Fail Criteria

**Pass:**
- Skill created successfully without asking for project_id or user_id
- Skill appears only in the current project (Project A)
- Skill is not visible in other projects (Project B)

**Fail:**
- User was asked to specify project_id or user_id manually
- Skill created in wrong project
- Skill appears in multiple projects
