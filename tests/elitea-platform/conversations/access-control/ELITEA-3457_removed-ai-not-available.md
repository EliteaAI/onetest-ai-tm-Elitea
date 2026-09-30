---
id: ELITEA-3457
title: "Removed AI Participant Not Available in Conversation"
priority: critical
type: functional
module: conversations
status: ready
execution_type: manual
tags: [feat:chat, access-control, restrict-access, ai-participants, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6283, EliteaAI/elitea_issues#6795]
---
# ELITEA-3457: Removed AI Participant Not Available in Conversation

**Module:** Conversations · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that an AI participant removed via Restrict Access wizard is no longer available to invoke in the conversation.

**Note:** Related to Bug #6795 - AI may persist visually until refresh

## Preconditions

- Logged in to {{base_url}} as conversation creator/author
- Conversation has 2 AI participants: AI-Agent-1 and AI-Agent-2
- Both AI agents can be invoked (@mentioned) in the conversation

## Test Data

| Field | Value |
|-------|-------|
| AI-Agent-1 | To be removed |
| AI-Agent-2 | To be retained |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open conversation | Conversation displays |
| 2 | Verify AI-Agent-1 can be invoked | Type @ and see AI-Agent-1 in suggestions |
| 3 | Open Restrict Access wizard | Wizard displays with both AI agents |
| 4 | Click (x) on AI-Agent-1 chip | AI-Agent-1 removed from selection |
| 5 | Keep AI-Agent-2 selected | AI-Agent-2 remains |
| 6 | Click "Restrict access" button | Restriction applied |
| 7 | Verify conversation participant list | AI-Agent-1 NOT shown in participants |
| 8 | Type @ to see available mentions | AI-Agent-1 NOT in suggestions |
| 9 | Verify AI-Agent-2 still available | AI-Agent-2 IS in suggestions |
| 10 | Try to manually type @AI-Agent-1 | Agent not recognized / no action |
| 11 | Refresh page | Changes persist |
| 12 | Repeat steps 7-10 | Same results after refresh |

## Expected Final State

- Removed AI agent cannot be invoked
- Retained AI agent works normally
- Changes persist after refresh

## Teardown

- None required
