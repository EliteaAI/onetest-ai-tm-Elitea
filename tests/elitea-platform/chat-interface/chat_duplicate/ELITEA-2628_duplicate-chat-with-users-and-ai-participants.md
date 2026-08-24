---
id: ELITEA-2628
title: "Duplicate Chat with Users and AI Participants - All Preserved"
priority: medium
type: functional
module: chat-interface
status: ready
execution_type: manual
automation_test_id: []
tags: [chat, duplicate, mixed-participants, team-project, P1]
requirements: [3837]
---
# ELITEA-2628: Duplicate Chat with Users and AI Participants - All Preserved

**Module:** Chat Interface · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that duplicating a chat with both user participants and AI participants in a team project preserves all participant types correctly.

## Preconditions

- User is logged in to {{base_url}}
- Team project context (multiple users available)
- Chat exists with both user participants (2+) and AI participants
- All participant types represented

## Test Data

- URL: {{base_url}}
- Team project
- Original chat with:
  - User A (creator)
  - User B, User C (participants)
  - Agent participant
  - Pipeline participant
  - Toolkit participant

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open chat in team project with mixed participants | Chat displays with users and AI |
| 2 | Document all user participants (Users A, B, C) | Note all user names |
| 3 | Document all AI participants (Agent, Pipeline, Toolkit) | Note all AI types |
| 4 | Duplicate the chat | Duplicate created successfully |
| 5 | Open duplicated chat | Duplicated chat opens |
| 6 | Verify User A present in duplicated chat | User A copied |
| 7 | Verify User B present in duplicated chat | User B copied |
| 8 | Verify User C present in duplicated chat | User C copied |
| 9 | Verify Agent participant present | Agent copied with configuration |
| 10 | Verify Pipeline participant present | Pipeline copied |
| 11 | Verify Toolkit participant present | Toolkit copied |
| 12 | Verify no participants missing | All original participants present |

## Expected Final State

- All user participants copied (A, B, C)
- All AI participants copied (Agent, Pipeline, Toolkit)
- No participants missing
- Mixed participant type preserved
- Chat functional with all participants

## Pass/Fail Criteria

**Pass:**
- All user participants present in duplicate (Bug #6256 validation)
- All AI participants present in duplicate
- No participant type missing
- All participants functional
- Correct participant count

**Fail:**
- Any user missing (especially Bug #6256: only creator)
- Any AI participant missing
- Participant type not preserved
- Configuration lost
- Participant count mismatch
