---
id: ELITEA-3315
title: "Project Context Builder receives runtime_context and creates context in current project only"
priority: critical
type: functional
module: project-context
status: ready
execution_type: automated
automation_test_id: [tests.ui.chat.test_chat_project_context_cross_project_isolation.TestChatProjectContextCrossProjectIsolation.test_project_context_isolated_to_current_project]
automation_pr: https://github.com/EliteaAI/elitea-testing-public/commit/09221399e77424ecedc778e2579d45233697940b
tags: [feat:context-management, feat:toolkits, story:6306, r-2.0.6, runtime-context, project-context-builder]
requirements: [EliteaAI/elitea_issues#6306]
---

# ELITEA-3315: Project Context Builder receives runtime_context and creates context in current project only

## Preconditions

- User is logged in to `{{base_url}}`
- Project Context Builder module is enabled in Chat Modules
- User is in Project A (note the project name/id)
- Project A does not have existing Project Context configured
- User has access to at least one other project (Project B)

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Confirm you are in Project A by checking the project selector | Project A is selected |
| 2 | Open Chat Modules menu and enable Project Context Builder | Project Context Builder toggle is enabled |
| 3 | Send: "Create project context: This is a QA automation project using Python and Playwright" | The assistant proceeds with Project Context creation without asking for project specification |
| 4 | Verify the Project Context chip/link appears in the chat response | Context chip is present |
| 5 | Navigate to Project A's Settings > Project Context | The created context content is present and enabled |
| 6 | Navigate to Project B's Settings > Project Context | Project B's context is unchanged (empty or previous content) |

## Expected Final State

Project Context Builder automatically receives runtime_context containing user_id and project_id, creating the context in the correct project without requiring explicit user input. The context is isolated to the current project only.

## Pass/Fail Criteria

**Pass:**
- Project Context created successfully without asking for project_id or user_id
- Context appears only in the current project (Project A)
- Other projects' context is unaffected (Project B)

**Fail:**
- User was asked to specify project_id or user_id manually
- Context created in wrong project
- Multiple projects affected unexpectedly
