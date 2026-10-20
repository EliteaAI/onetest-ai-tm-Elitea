---
id: ELITEA-3366
title: "Skill creation from chat with complete information creates skill and chip opens in Canvas"
priority: critical
type: functional
module: chat-interface
status: ready
execution_type: automated
automation_test_id: tests.ui.chat.test_skill_creation_from_chat_chip_canvas.TestSkillCreationFromChat.test_skill_created_from_chat_chip_opens_canvas
automation_pr: https://github.com/EliteaAI/elitea-testing-public/commit/7509c72970efca36faddc66501b255f4db3153f8
tags: [feat:chat, story:6239, regression, skills-builder, happy-path, canvas]
requirements: [EliteaAI/elitea_issues#6239]
---

# ELITEA-3366: Skill creation from chat with complete information creates skill and chip opens in Canvas

## Objective

Verify that a fully specified Skill creation request via chat creates the Skill without clarification, displays a chip in the response, and the chip opens the Skill in Canvas mode.

## Preconditions

- User is logged in to `{{base_url}}`
- Skills Builder is enabled in Chat Modules
- Canvas mode is available

## Test Data

| Field | Value |
|-------|-------|
| Skill name | Daily Standup Summarizer |
| Description | Summarizes daily standup notes into action items |
| Instructions | Given raw standup notes, extract blockers, decisions, and action items as a bulleted list |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Send a chat message providing Skill name, description, and instructions in full: "Create a skill called 'Daily Standup Summarizer' that summarizes daily standup notes into action items. Instructions: Given raw standup notes, extract blockers, decisions, and action items as a bulleted list." | Assistant proceeds to create the Skill without asking clarifying questions |
| 2 | Verify chat response contains a Skill chip | A "Skill: Daily Standup Summarizer" chip/link is displayed in the chat response |
| 3 | Click the Skill chip/link | Canvas mode opens displaying the Skill |
| 4 | Verify Skill fields in Canvas | Name: "Daily Standup Summarizer", Description and Instructions match what was provided |
| 5 | Open the conversation's participant list | The newly created Skill is NOT automatically added as a participant |

## Expected Final State

Skill is created with correct fields, chip is displayed, chip opens Canvas with accurate content, Skill not auto-added to participants.

## Pass/Fail Criteria

**Pass:**
- Skill created with correct Name/Description/Instructions
- Skill chip/link shown in chat response
- No clarifying question shown (information was complete)
- Clicking chip opens Skill in Canvas mode with correct content
- Skill not added to participant list

**Fail:**
- Skill not created or created with incorrect/missing fields
- Clarifying question shown despite complete information
- Chip missing or fails to open Canvas
- Canvas shows incorrect/stale content
- Skill auto-added to participants
