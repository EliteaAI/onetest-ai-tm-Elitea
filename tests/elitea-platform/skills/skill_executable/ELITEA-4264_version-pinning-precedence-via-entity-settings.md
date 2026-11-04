---
id: ELITEA-4264
title: "Version Pinning Precedence via entity_settings"
priority: critical
type: functional
module: skills
status: ready
execution_type: manual
tags: [skills, chat, participants, versioning, backend, api]
requirements: [#6923]
---
# ELITEA-4264: Version Pinning Precedence via entity_settings

**Module:** Skills · **Priority:** Critical · **Type:** Functional

**Objective:** Verify entity_settings.version_id overrides skill's default version for inference

## Preconditions

- Valid project exists (e.g., `project_id: 9`)
- Skill exists with multiple versions (e.g., `version_id: 1` as default, `version_id: 2` available)
- Each version has distinct behavior (e.g., different system prompts or models)
- Authentication token available

## Test Data

- Project ID: 9
- Skill ID: `<valid_skill_id>`
- Default version ID: 1
- Pinned version ID: 2
- Test message: "Test version response"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Send GET request to `/api/v1/skills/<skill_id>` to confirm default version | API returns skill metadata with `default_version_id: 1` |
| 2 | Create first chat with skill participant WITHOUT `version_id` in `entity_settings`: `{"project_id": 9, "participants": [{"type": "skill", "entity_id": "<skill_id>", "entity_settings": {"chat_history_template": "all"}}]}` | Chat created successfully with participant showing no explicit `version_id` in settings |
| 3 | Send message to first chat and verify which version responds | Skill responds using default version (version 1) — verify by checking response characteristics or usage logs |
| 4 | Create second chat with skill participant WITH pinned `version_id` in `entity_settings`: `{"project_id": 9, "participants": [{"type": "skill", "entity_id": "<skill_id>", "entity_settings": {"version_id": 2, "chat_history_template": "all"}}]}` | Second chat created successfully with participant showing `entity_settings.version_id: 2` |
| 5 | Send identical message to second chat and verify which version responds | Skill responds using pinned version (version 2) — response differs from step 3, confirming version override |
| 6 | Query database or GET `/api/v1/usage?entity_type=skill&entity_id=<skill_id>` to confirm versions used | Usage records show: First chat used `version_id: 1` (default), Second chat used `version_id: 2` (pinned via entity_settings) |

## Expected Final State

- Two chats exist with different version behaviors
- Database records reflect correct version attribution
- entity_settings.version_id precedence confirmed over default version

## Pass/Fail Criteria

PASS: Chat without version_id uses default version, chat with pinned version_id uses that version, usage records confirm correct version attribution
FAIL: Version pinning ignored, both chats use same version, usage records show incorrect version_id, API errors
