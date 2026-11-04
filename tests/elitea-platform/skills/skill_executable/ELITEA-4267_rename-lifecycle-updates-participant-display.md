---
id: ELITEA-4267
title: "Rename Lifecycle Updates Participant Display"
priority: high
type: functional
module: skills
status: ready
execution_type: manual
tags: [skills, chat, participants, lifecycle, rename, backend, api]
requirements: [#6923]
---
# ELITEA-4267: Rename Lifecycle Updates Participant Display

**Module:** Skills · **Priority:** High · **Type:** Functional

**Objective:** Verify renamed skill updates participant display name in existing chats

## Preconditions

- Valid project exists (e.g., `project_id: 9`)
- Skill exists with original name (e.g., "Customer Support Skill")
- User has permission to rename skill

## Test Data

- Project ID: 9
- Skill ID: `<valid_skill_id>`
- Original skill name: "Customer Support Skill"
- Updated skill name: "Updated Support Skill"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Create chat with skill participant: POST `/api/v1/chats` | Chat created successfully |
| 2 | Send GET `/api/v1/chats/<chat_id>/participants` before rename | Participant shows `display_name: "Customer Support Skill"` (or equivalent field), correct `entity_id` |
| 3 | Send GET `/api/v1/skills/<skill_id>` before rename | Skill metadata shows `name: "Customer Support Skill"` |
| 4 | Rename the skill: PATCH `/api/v1/skills/<skill_id>` with `{"name": "Updated Support Skill"}` | API returns 200 OK with updated skill metadata |
| 5 | Send GET `/api/v1/chats/<chat_id>/participants` after rename | Participant shows UPDATED name: `display_name: "Updated Support Skill"`, same `entity_id` (unchanged), other fields unchanged |
| 6 | Send GET `/api/v1/skills/<skill_id>` after rename | Skill metadata shows `name: "Updated Support Skill"` |
| 7 | Send message to chat and verify skill responds | Skill responds normally, UI can display updated name |
| 8 | Create NEW chat with renamed skill and verify participant name | New chat participant shows `display_name: "Updated Support Skill"` (consistent) |

## Expected Final State

- Skill renamed in database
- All existing chats reflect new name
- Participant `entity_id` remains stable
- No duplicate participants created

## Pass/Fail Criteria

PASS: Skill renamed successfully, all existing chat participants show updated name, new chats show updated name, entity_id stable
FAIL: Rename fails, existing chats show old name, new chats show old name, entity_id changed, duplicate participants created, API errors
