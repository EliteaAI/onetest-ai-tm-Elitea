---
id: ELITEA-3769
title: "Export Conversation With User-to-User Messages"
priority: medium
type: functional
module: conversations
status: ready
execution_type: manual
tags: [eng:frontend, eng:backend, feat:chat, feat:export, r-2.0.8]
requirements: [EliteaAI/elitea_issues#4590]
---
# ELITEA-3769: Export Conversation With User-to-User Messages

**Module:** Conversations · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that conversations between multiple human users export correctly with all participant data.

**Coverage:**
- User-to-user conversations export successfully
- All human participants represented in export
- User metadata (names, identifiers) preserved
- Message chronology maintained across multiple users

## Preconditions

- Logged in to {{base_url}}
- Conversation exists with multiple human users (no AI agents)
- At least 3 human participants in conversation
- User is the conversation creator

## Test Data

- Conversation with at least 3 human participants (e.g., User A, User B, User C)
- At least 10 messages exchanged between users

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chats section | Chat list displays |
| 2 | Identify user-to-user conversation | Verify Participants panel shows only human users (no AI agents) |
| 3 | Right-click conversation | Context menu with "Export" appears |
| 4 | Click "Export" | Dialog opens |
| 5 | Click "Export" | JSON file downloads |
| 6 | Open JSON file in text editor | JSON structure visible |
| 7 | Verify all messages from all users included | Messages from User A, User B, and User C all present |
| 8 | Verify user metadata - Sender names | Each message shows correct sender name |
| 9 | Verify user metadata - User identifiers | User IDs or emails included in metadata |
| 10 | Verify all participants represented | All 3 users (A, B, C) appear in messages |
| 11 | Verify message order | Chronological order maintained across all users |
| 12 | Verify timestamps for all messages | All messages have timestamps |
| 13 | Verify participant list in JSON | JSON includes list of all conversation participants |
| 14 | Verify no messages missing | Message count matches conversation |

## Expected Final State

- JSON contains all messages from all human users
- User metadata (names, IDs) correct for each message
- Chronological order maintained
- All participants represented

## Pass/Fail Criteria

**Pass:**
- All user messages exported
- Sender metadata correct (names, IDs)
- All participants (User A, B, C) represented
- Chronological order correct
- Timestamps present for all messages

**Fail:**
- Messages from one or more users missing
- User metadata incorrect or missing
- Participants not all represented
- Message order incorrect
- Missing timestamps

## Postconditions

- Original conversation unchanged
- All users retain access to conversation
