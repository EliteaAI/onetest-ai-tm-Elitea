---
id: ELITEA-4401
title: "New chat from default template with multiple participants has no active participant"
priority: critical
type: functional
module: chat-templates/skills
status: ready
execution_type: manual
tags: [user_story:6925, feat:skills, feat:chat-templates, skills-in-templates]
requirements: [EliteaAI/elitea_issues#6925]
---
# ELITEA-4401: New Chat from Default Template with Multiple Participants

**Module:** Chat Templates / Skills · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that when a default template contains multiple participants (agent, skill, toolkit), creating a new chat does NOT auto-select any participant as active, requiring manual selection.

## Preconditions

- User is logged in
- Navigate to Settings → General → Chat templates
- Create a default template with 3 participants: 1 agent, 1 skill, 1 toolkit
- Check "Set as default" checkbox

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/new-chat` |
| Template Name | Multiple Participants Template |
| Agent | Any available agent |
| Skill | Any available skill |
| Toolkit | Any available toolkit |
| Set as Default | Yes (checked) |
| Test Message | Help me with this task |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to New Chat page | New chat interface loads |
| 2 | Verify the default template is applied automatically | Default template applied, participants loaded |
| 3 | Check the participants section in the new chat interface | Participants panel displays on right side |
| 4 | Verify all 3 participants (agent, skill, toolkit) appear as pinned | All 3 participants visible with correct icons |
| 5 | Verify NO participant is marked as active (no highlighting on any participant) | No participant highlighted or selected |
| 6 | Click on the skill participant to make it active | Skill becomes clickable |
| 7 | Verify the skill becomes highlighted/selected | Skill is now visibly highlighted as active |
| 8 | Type and send a message: "Help me with this task" | Message typed and sent |
| 9 | Verify the message is sent to the selected skill | Message shows as sent to selected skill |
| 10 | Verify the skill responds correctly | Skill response appears in chat |

## Expected Final State

- All template participants load in new chat interface
- NO participant is active by default when multiple participants exist
- All participants show as pinned with correct icons
- User can manually select any participant to activate
- Selected participant receives messages and responds
- Conversation is created with all template participants intact

## Pass/Fail Criteria

**Pass:**
- All 3 participants load in new chat
- No participant active by default
- All participants pinned correctly
- User can manually select participant
- Selected participant receives messages
- Conversation created with all participants

**Fail:**
- Not all participants load
- One participant auto-selected as active
- Participants not pinned correctly
- Cannot manually select participant
- Messages not sent to selected participant
- Conversation missing participants

**Coverage:** AC 4, AC 5
