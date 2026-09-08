---
id: ELITEA-3314
title: "Chat informs user it can only create skill/context within current project when different project requested"
priority: medium
type: functional
module: project-context
status: ready
execution_type: manual
tags: [feat:context-management, feat:toolkits, story:6306, r-2.0.6, error-handling, scope-limitation]
requirements: [EliteaAI/elitea_issues#6306]
---

# ELITEA-3314: Chat informs user it can only create skill/context within current project when different project requested

## Preconditions

- User is logged in to `{{base_url}}`
- Skills Builder and Project Context Builder modules are enabled
- User is in Project A
- User has access to another project (Project B) and knows its name/id

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Confirm you are in Project A | Project A is selected |
| 2 | Enable Skills Builder in Chat Modules | Module enabled |
| 3 | Send: "Create a skill called 'Test Skill' in Project B" (explicitly requesting different project) | Chat responds that it can only create skills within the current project |
| 4 | Verify no skill was created in Project B | Project B's Skills list does not contain "Test Skill" |
| 5 | Enable Project Context Builder | Module enabled |
| 6 | Send: "Create project context for Project B: This is a test context" | Chat responds that it can only create/update project context within the current project |
| 7 | Verify Project B's context was not modified | Project B's Settings > Project Context is unchanged |

## Expected Final State

When a user explicitly requests to create a skill or project context in a different project than the current one, the chat clearly informs them that this operation is limited to the current project scope.

## Pass/Fail Criteria

**Pass:**
- Clear message explaining the current-project-only limitation
- No skill/context created in the requested different project
- User understands why the request was not fulfilled as specified

**Fail:**
- Skill/context silently created in wrong project
- Cryptic error message without explanation
- No feedback to user about the scope limitation
