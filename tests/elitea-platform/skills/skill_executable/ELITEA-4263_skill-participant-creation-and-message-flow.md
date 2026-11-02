---
id: ELITEA-4263
title: "Skill Participant Creation & Message Flow"
priority: critical
type: functional
module: skills
status: ready
execution_type: manual
tags: [skills, chat, participants, backend, api]
requirements: [#6923]
---
# ELITEA-4263: Skill Participant Creation & Message Flow

**Module:** Skills · **Priority:** Critical · **Type:** Functional

**Objective:** Verify skill participant creation and message exchange via tool-less LLM chat path

## Preconditions

- Valid project exists (e.g., `project_id: 9`)
- At least one published skill exists in the project with a valid version
- Authentication token available for API requests
- Database schema supports `ParticipantTypes.skill`

## Test Data

- Project ID: 9
- Skill ID: `<valid_skill_id>`
- Test message: "Hello skill participant"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Send POST request to `/api/v1/chats` with skill participant payload: `{"project_id": 9, "participants": [{"type": "skill", "entity_id": "<skill_id>", "entity_settings": {"chat_history_template": "all"}}]}` | API returns 201 Created with chat object containing `chat_id`, `participants` array with skill participant showing `type: "skill"`, `entity_id`, and `entity_settings` |
| 2 | Verify skill participant persisted in database | Database record shows correct `type: "skill"` field |
| 3 | Send POST request to `/api/v1/chats/<chat_id>/messages` with user message: `{"content": "Hello skill participant", "sender_type": "user"}` | API returns 201 Created with message object containing `message_id`, `content`, `sender_type: "user"` |
| 4 | Poll GET `/api/v1/chats/<chat_id>/messages` or listen to streaming endpoint | Skill participant response message appears within 30s timeout |
| 5 | Verify skill response contains correct attributes | Response shows `sender_type: "skill"`, `content` field populated (LLM-generated), no tool invocations present (tool-less LLM chat path) |
| 6 | Send GET request to `/api/v1/chats/<chat_id>/participants` | API returns participant list with skill participant showing correct `entity_id`, `type: "skill"`, and metadata |

## Expected Final State

- Chat exists with skill participant
- Message history contains user and skill messages
- Database reflects correct participant type and message attribution

## Pass/Fail Criteria

PASS: Skill participant created successfully, messages exchanged via tool-less LLM path, all API responses contain correct structure and data
FAIL: Participant creation fails, messages not delivered, skill response missing, incorrect participant type stored, tool invocations present
