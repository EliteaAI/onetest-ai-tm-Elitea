---
id: ELITEA-4265
title: "Usage Attribution with entity_type: 'skill'"
priority: critical
type: functional
module: skills
status: ready
execution_type: manual
tags: [skills, chat, participants, usage, attribution, backend, api]
requirements: [#6923]
---
# ELITEA-4265: Usage Attribution with entity_type: 'skill'

**Module:** Skills · **Priority:** Critical · **Type:** Functional

**Objective:** Verify usage records correctly attribute skill participant interactions with proper entity_type, entity_id, and version_id

## Preconditions

- Valid project exists (e.g., `project_id: 9`)
- Skill exists with known version (e.g., `version_id: 5`)
- Usage tracking system operational
- Access to usage API or database

## Test Data

- Project ID: 9
- Skill ID: `<valid_skill_id>`
- Version ID: 5 (pinned)
- Test message: "Test usage tracking"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Create chat with skill participant, pinning specific version: `{"project_id": 9, "participants": [{"type": "skill", "entity_id": "<skill_id>", "entity_settings": {"version_id": 5, "chat_history_template": "all"}}]}` | Chat created successfully with skill participant and pinned version_id: 5 |
| 2 | Send POST request to `/api/v1/chats/<chat_id>/messages` with test message | Message sent successfully |
| 3 | Wait for skill response completion | Skill response received with LLM-generated content |
| 4 | Query usage records: GET `/api/v1/usage?project_id=9&entity_type=skill&entity_id=<skill_id>` | API returns usage records filtered by `entity_type: 'skill'` |
| 5 | Verify usage record contains required attribution fields | Record shows: `entity_type: 'skill'`, `entity_id: <skill_id>`, `version_id: 5`, `project_id: 9`, token counts (prompt_tokens, completion_tokens, total_tokens), timestamp, model name |
| 6 | Compare with agent participant usage records for schema consistency | Usage record structure matches agent usage records (consistent schema across participant types) |

## Expected Final State

- Usage records persisted with correct skill attribution
- Billing/analytics systems can distinguish skill usage from agent usage
- Version-specific usage is trackable

## Pass/Fail Criteria

PASS: Usage records contain correct entity_type='skill', proper entity_id, version_id matches pinned version, all required fields present, schema consistent with agent usage
FAIL: Usage records missing or incorrect, entity_type wrong, version_id mismatch, required fields missing, schema inconsistent
