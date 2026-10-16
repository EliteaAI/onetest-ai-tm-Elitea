---
id: ELITEA-3946
title: "AI-Only Duplicated Chat Does Not Add Unintended User Participants"
priority: medium
type: functional
module: chat-interface
status: ready
execution_type: manual
tags: [chat, duplicate, ai-only, user-isolation, P1]
requirements: [3837]
---
# ELITEA-3946: AI-Only Duplicated Chat Does Not Add Unintended User Participants

**Module:** Chat Interface · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that duplicating an AI-only chat does not automatically add unintended human users as participants.

## Preconditions

- User is logged in to {{base_url}}
- Private project OR team project chat with only AI participants
- No human user participants in original chat (except owner)

## Test Data

- URL: {{base_url}}
- Chat with AI participants only (Agent/Pipeline/Toolkit/MCP)
- Private project context preferred

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open a chat with AI participants only | Chat contains Agent/Pipeline/Toolkit/MCP only |
| 2 | Verify no additional user participants in Users section | Only chat owner, no other users |
| 3 | Duplicate the chat | Duplicate created successfully |
| 4 | Open duplicated chat | Duplicated chat opens |
| 5 | Open the Participants panel | Participants panel displays |
| 6 | Check the USERS section | Verify only the owner user present |
| 7 | Verify no additional users were added | No unintended team members added |
| 8 | Check AGENTS section | Only original AI participants present |
| 9 | Verify total participant count matches expected | Count = Owner + AI participants |

## Expected Final State

- Duplicated chat contains only intended participants
- No automatic addition of team members
- AI participants preserved
- User participant list clean (owner only in private project)

## Pass/Fail Criteria

**Pass:**
- Only AI participants and owner present
- No unintended users added to duplicate
- Participant count matches original
- AI-only nature preserved

**Fail:**
- Additional users automatically added
- Team members added without explicit action
- Participant list contaminated
- Owner missing from duplicate
