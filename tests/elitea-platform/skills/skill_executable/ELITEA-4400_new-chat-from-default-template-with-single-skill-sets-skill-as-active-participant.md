---
id: ELITEA-4400
title: "New chat from default template with single skill sets skill as active participant"
priority: critical
type: functional
module: chat-templates/skills
status: ready
execution_type: manual
tags: [user_story:6925, feat:skills, feat:chat-templates, skills-in-templates]
requirements: [EliteaAI/elitea_issues#6925]
---
# ELITEA-4400: New Chat from Default Template with Single Skill

**Module:** Chat Templates / Skills · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that when a default template contains exactly one skill participant, creating a new chat automatically sets that skill as the active participant.

## Preconditions

- User is logged in
- Navigate to Settings → General → Chat templates
- Create a template with exactly ONE participant: a skill (e.g., "Code Reviewer")
- Check "Set as default" checkbox when creating the template

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/new-chat` |
| Template Name | Single Skill Template |
| Skill | Code Reviewer |
| Set as Default | Yes (checked) |
| Test Message | Review this code: print('hello') |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to New Chat page | New chat interface loads |
| 2 | Verify the default template is applied automatically | Default template applied, participants loaded |
| 3 | Check the participants section in the new chat interface | Participants panel displays on right side |
| 4 | Verify the skill "Code Reviewer" appears as a pinned participant | Skill appears with correct icon and name |
| 5 | Verify the skill is set as the ACTIVE participant (highlighted/selected) | Skill is visibly highlighted as active |
| 6 | Type a message in the chat input: "Review this code: print('hello')" | Message typed in input field |
| 7 | Send the message | Message sent successfully |
| 8 | Verify the message is sent to the skill | Message shows as sent to "Code Reviewer" |
| 9 | Verify the skill responds to the message | Skill response appears in chat |
| 10 | Verify the conversation is created with the skill participant | Conversation saved with skill as participant |

## Expected Final State

- Default template with single skill is automatically applied to new chat
- Skill appears as pinned participant with correct icon
- Skill is set as active participant (visibly highlighted/selected)
- Messages are routed to the skill automatically
- Skill can respond to messages
- Conversation saves with skill as participant

## Pass/Fail Criteria

**Pass:**
- Default template automatically applied
- Skill appears as pinned participant
- Skill is active by default (highlighted)
- Messages sent to skill successfully
- Skill responds correctly
- Conversation created with skill

**Fail:**
- Template not applied automatically
- Skill not appearing in participants
- Skill not active by default
- Messages not routed to skill
- Skill cannot respond
- Conversation not created properly

**Coverage:** AC 4, AC 5
