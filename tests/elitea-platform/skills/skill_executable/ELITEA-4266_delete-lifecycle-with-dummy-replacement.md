---
id: ELITEA-4266
title: "Delete Lifecycle with Dummy Replacement"
priority: high
type: functional
module: skills
status: ready
execution_type: manual
tags: [skills, chat, participants, lifecycle, delete, backend, api]
requirements: [#6923]
---
# ELITEA-4266: Delete Lifecycle with Dummy Replacement

**Module:** Skills · **Priority:** High · **Type:** Functional

**Objective:** Verify deleted skill is replaced with dummy participant while preserving chat history

## Preconditions

- Valid project exists (e.g., `project_id: 9`)
- Skill exists with at least one version
- User has permission to delete skill

## Test Data

- Project ID: 9
- Skill ID: `<valid_skill_id>`
- Number of test messages: 3 user + 3 skill responses (6 total)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Create chat with skill participant and exchange 3 messages (user sends 3, skill responds 3 times) | Chat created with 6 messages total (3 user, 3 skill responses) |
| 2 | Send GET `/api/v1/chats/<chat_id>/participants` before deletion | Participant list shows: `type: "skill"`, `entity_id: <skill_id>`, active status |
| 3 | Send GET `/api/v1/chats/<chat_id>/messages` before deletion | Message history shows 6 messages with correct `sender_type` attribution |
| 4 | Delete the skill: DELETE `/api/v1/skills/<skill_id>` | API returns 200/204 confirming skill deletion |
| 5 | Send GET `/api/v1/chats/<chat_id>/participants` after deletion | Participant still exists but marked as dummy/deleted with display name updated (e.g., "Deleted Skill"), original `entity_id` preserved or reference updated |
| 6 | Send GET `/api/v1/chats/<chat_id>/messages` after deletion | Message history UNCHANGED: All 6 messages still present, historical `sender_type: "skill"` preserved, message content intact |
| 7 | Attempt to send new message to chat: POST `/api/v1/chats/<chat_id>/messages` | Message either succeeds but receives no response from dummy participant, OR returns error indicating participant unavailable |
| 8 | Verify dummy participant behavior | Dummy participant does NOT invoke LLM or generate responses |

## Expected Final State

- Skill deleted from project
- Chat history fully preserved (all messages intact)
- Dummy participant prevents chat breakage
- No orphaned messages

## Pass/Fail Criteria

PASS: Skill deleted, participant replaced with dummy, all chat history preserved, dummy does not generate responses
FAIL: Chat history lost, messages deleted, participant completely removed, new messages generate responses from deleted skill, errors accessing chat
