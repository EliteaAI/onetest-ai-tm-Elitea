---
id: ELITEA-3770
title: "Export Conversation With Mixed AI and Human Participants"
priority: high
type: functional
module: conversations
status: ready
execution_type: manual
tags: [eng:frontend, eng:backend, feat:chat, feat:export, feat:agents, r-2.0.8]
requirements: [EliteaAI/elitea_issues#4590]
---
# ELITEA-3770: Export Conversation With Mixed AI and Human Participants

**Module:** Conversations · **Priority:** High · **Type:** Functional

**Objective:** Verify that conversations with both AI agents and human users export correctly with proper participant differentiation.

**Coverage:**
- Mixed participant conversations (AI + humans) export successfully
- Participant types clearly differentiated in JSON
- All messages from all participant types included
- Chronological order maintained across participant types

## Preconditions

- Logged in to {{base_url}}
- Conversation exists with both human users and AI agents
- At least 2 human users + 1 AI agent in conversation
- User is the conversation creator

## Test Data

- Conversation participants:
  - 2 human users (e.g., User A, User B)
  - 1 AI agent (e.g., Agent X or Pipeline Y)
- At least 12 messages exchanged (mixed from all participants)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chats section | Chat list displays |
| 2 | Identify mixed participant conversation | Participants panel shows both humans + AI (icons/labels indicating each type) |
| 3 | Right-click conversation | Context menu with "Export" appears |
| 4 | Click "Export" | Dialog opens |
| 5 | Click "Export" | File downloads (JSON or ZIP) |
| 6 | Open JSON file | JSON structure visible |
| 7 | Verify all messages from all participants included | Messages from User A, User B, and Agent X all present |
| 8 | Verify participant differentiation - Human messages | Human messages have user metadata: user type, name, user ID |
| 9 | Verify participant differentiation - AI messages | AI messages have agent metadata: agent type, agent name, model info (if applicable) |
| 10 | Verify message order | Chronological order maintained across all participant types |
| 11 | Verify no participant data missing | All humans (User A, B) and AI agents (Agent X) represented |
| 12 | Verify participant list in JSON metadata | JSON includes complete participant list with types indicated |
| 13 | If AI generated artifacts | Verify artifacts metadata included in JSON |
| 14 | Verify timestamps for all messages | All messages (human and AI) have timestamps |

## Expected Final State

- JSON contains all messages from both humans and AI agents
- Participant types clearly differentiated in metadata
- Chronological order maintained
- All participants represented

## Pass/Fail Criteria

**Pass:**
- All messages from all participants exported
- Human vs AI participants clearly differentiated
- Metadata correct for each participant type
- Chronological order maintained
- All participants represented in JSON

**Fail:**
- Messages from humans or AI missing
- Participant types not differentiated
- Metadata missing or incorrect
- Message order broken
- Participants not all represented

## Postconditions

- Original conversation unchanged
- All participants (human and AI) remain functional
