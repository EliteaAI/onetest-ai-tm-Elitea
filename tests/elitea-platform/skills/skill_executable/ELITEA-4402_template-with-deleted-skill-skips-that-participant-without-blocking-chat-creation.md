---
id: ELITEA-4402
title: "Template with deleted skill skips that participant without blocking chat creation"
priority: critical
type: functional
module: chat-templates/skills
status: ready
execution_type: manual
tags: [user_story:6925, feat:skills, feat:chat-templates, skills-in-templates]
requirements: [EliteaAI/elitea_issues#6925]
---
# ELITEA-4402: Template with Deleted Skill Skips Participant

**Module:** Chat Templates / Skills · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that when a skill in a default template is deleted, chat creation proceeds without errors, displays an info toast, and loads only valid participants.

## Preconditions

- Default template exists with 2 participants: 1 agent and 1 skill "Code Reviewer"
- User with permissions to delete skills
- User is logged in

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/settings` and `{{base_url}}/app/new-chat` |
| Template Name | Template with Agent and Skill |
| Agent | Any available agent |
| Skill to Delete | Code Reviewer |
| Set as Default | Yes (checked) |
| Test Message | Hello |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Settings → General → Chat templates and note the skill in the template | Template shows agent and "Code Reviewer" skill |
| 2 | Navigate to Skills section | Skills page loads |
| 3 | Delete "Code Reviewer" skill and confirm the deletion | Skill deleted successfully |
| 4 | Navigate to New Chat page | New chat interface loads |
| 5 | Observe if an info toast appears: "1 template participant(s) were skipped" | Info toast displays with correct message |
| 6 | Verify only the agent participant is loaded (no skill present) | Only agent appears in PARTICIPANTS panel |
| 7 | Verify chat interface loads without errors | Chat interface functional, no error messages |
| 8 | Type and send a message to the agent: "Hello" | Message typed and sent |
| 9 | Verify the agent responds successfully | Agent response appears in chat |
| 10 | Verify the conversation is created with only the valid participant (agent) | Conversation saved with agent only |

## Expected Final State

- Info toast notifies user: "1 template participant(s) were skipped"
- Deleted skill does not appear in new chat participants
- Remaining valid participant (agent) loads correctly
- Chat creation proceeds without blocking or errors
- User can interact with remaining participants normally
- Conversation saves successfully with valid participants only

## Pass/Fail Criteria

**Pass:**
- Info toast displays correct message
- Deleted skill not in participants
- Agent loads correctly
- Chat creation not blocked
- User can interact with agent
- Conversation saves with valid participant

**Fail:**
- No info toast displayed
- Deleted skill still appears
- Agent not loaded
- Chat creation blocked or errors
- Cannot interact with remaining participant
- Conversation not created properly

**Coverage:** AC 6
