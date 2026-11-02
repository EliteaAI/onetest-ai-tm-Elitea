---
id: ELITEA-4268
title: "Regression - Existing Participant Types Unaffected"
priority: critical
type: regression
module: skills
status: ready
execution_type: manual
tags: [skills, chat, participants, regression, agents, backend, api]
requirements: [#6923]
---
# ELITEA-4268: Regression - Existing Participant Types Unaffected

**Module:** Skills · **Priority:** Critical · **Type:** Regression

**Objective:** Verify existing agent and user participant types remain fully functional after skill participant implementation

## Preconditions

- Valid project exists (e.g., `project_id: 9`)
- At least one agent exists in project
- Existing chat with agent participant (created BEFORE skill participant feature)

## Test Data

- Project ID: 9
- Agent ID: `<valid_agent_id>`
- Skill ID: `<valid_skill_id>`
- Existing chat ID: `<chat_created_before_skill_feature>`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Send GET `/api/v1/chats/<existing_chat_id>` to retrieve existing agent chat (pre-skill feature) | Existing chat loads successfully, schema intact |
| 2 | Send POST `/api/v1/chats/<existing_chat_id>/messages` to send message to existing agent chat | Message sent successfully |
| 3 | Verify agent responds normally with tools enabled | Agent responds with normal behavior: tool invocations present (if applicable), correct message attribution (`sender_type: "agent"`), tools invoked as configured |
| 4 | Send GET `/api/v1/chats/<existing_chat_id>/participants` | Participant list shows `type: "agent"` (NOT affected by new skill type) |
| 5 | Create NEW chat with agent participant (post-skill feature): POST `/api/v1/chats` with `{"project_id": 9, "participants": [{"type": "agent", "entity_id": "<agent_id>", "entity_settings": {"chat_history_template": "all"}}]}` | New agent chat created successfully with `type: "agent"` participant |
| 6 | Send message to new agent chat and verify tool invocation works | Agent responds normally with tool invocations working |
| 7 | Query usage records: GET `/api/v1/usage?entity_type=agent` | Usage records show `entity_type: 'agent'` (distinct from skill usage) |
| 8 | Test agent delete/rename lifecycle | Agent delete → removes/archives participant correctly; rename → updates display name (existing behavior preserved) |
| 9 | Create chat with mixed participants (agent + skill): POST `/api/v1/chats` with both agent and skill participants | Chat created with both participant types successfully |
| 10 | Verify both participants can coexist and respond independently | Both participants respond independently: Agent with tools enabled, Skill with tool-less LLM chat path, no conflicts or attribution errors |

## Expected Final State

- Existing agent chats functional
- Agent participant type unchanged
- Usage attribution distinct between agent and skill
- Mixed participant chats work correctly
- Backward compatibility confirmed

## Pass/Fail Criteria

PASS: All agent functionality preserved, new agent chats work, usage attribution correct, mixed chats functional, no regression in existing features
FAIL: Agent chats broken, tool invocations fail, usage attribution incorrect, mixed chats error, any regression in pre-existing participant types
