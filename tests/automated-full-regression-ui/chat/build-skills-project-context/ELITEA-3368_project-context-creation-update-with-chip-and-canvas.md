---
id: ELITEA-3368
title: "Project Context creation and update from chat with chip opening in Canvas"
priority: critical
type: functional
module: chat-interface
status: ready
execution_type: automated
automation_test_id: [tests.ui.chat.test_chat_project_context_builder.TestChatProjectContextBuilder.test_create_and_update_project_context_via_chat_chip_canvas]
automation_pr: https://github.com/EliteaAI/elitea-testing-public/commit/09221399e77424ecedc778e2579d45233697940b
tags: [feat:chat, story:6239, regression, project-context-builder, happy-path, canvas]
requirements: [EliteaAI/elitea_issues#6239]
---

# ELITEA-3368: Project Context creation and update from chat with chip opening in Canvas

## Objective

Verify that Project Context can be created and updated via chat, displays a chip in the response, the chip opens in Canvas mode, and updates modify existing context instead of creating duplicates.

## Preconditions

- User is logged in to `{{base_url}}`
- Project Context Builder is enabled in Chat Modules
- The current project has no existing Project Context configured
- Canvas mode is available

## Test Data

| Field | Value |
|-------|-------|
| Context content (create) | "This project is a Python REST API for order management." |
| Update request | "Update the project context to mention we now support GraphQL in addition to REST." |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Send a chat message to create Project Context: "Create project context: This project is a Python REST API for order management." | Assistant proceeds to create the Project Context without asking clarifying questions |
| 2 | Verify chat response contains a Project Context chip | A "Project Context" chip/link is displayed in the chat response |
| 3 | Click the Project Context chip/link | Canvas mode opens displaying the Project Context |
| 4 | Verify Project Context content in Canvas | Content matches what was provided |
| 5 | Open the conversation's participant list | The newly created Project Context is NOT automatically added as a participant |
| 6 | Send an update request: "Update the project context to mention we now support GraphQL in addition to REST." | Assistant updates the existing Project Context |
| 7 | Verify chat response contains a Project Context chip | A Project Context chip/link is displayed, referencing the updated entity |
| 8 | Click the Project Context chip and verify content | The existing entity now includes the GraphQL detail |
| 9 | Navigate to Project Context list | No duplicate Project Context entity exists; only one updated entity |

## Expected Final State

Project Context is created with correct content, chip opens Canvas, updates modify existing entity in place without creating duplicates, not auto-added to participants.

## Pass/Fail Criteria

**Pass:**
- Project Context created with correct content
- Project Context chip/link shown in chat response
- Clicking chip opens Canvas mode with correct content
- Update modifies existing Project Context (no duplicate created)
- Updated content includes new information
- Project Context not added to participant list

**Fail:**
- Project Context not created or created with incorrect content
- Chip missing or fails to open Canvas
- Update creates duplicate instead of modifying existing
- Canvas shows incorrect/stale content
- Project Context auto-added to participants
