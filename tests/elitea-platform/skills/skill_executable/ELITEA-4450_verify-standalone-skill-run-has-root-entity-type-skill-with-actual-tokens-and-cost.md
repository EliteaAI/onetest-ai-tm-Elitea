---
id: ELITEA-4450
title: "Verify standalone skill run has root_entity_type='skill' with actual tokens and cost"
priority: critical
type: functional
module: usage-metering
status: ready
execution_type: manual
tags: [feat:skills, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6926]
---

## Preconditions

- User is logged in to `{{base_url}}`
- Database access to `usage_event` table
- Standalone skill runner API (S1) is available
- Test skill is published

## Test Data

| Field | Value |
|-------|-------|
| Skill name | `test-standalone-skill` |
| Skill ID | `<skill_id>` |
| Skill version ID | `<version_id>` |
| API endpoint | `{{base_url}}/api/v1/skills/run` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Execute skill standalone via S1 API: `POST /api/v1/skills/run` with `skill_id` | Skill run completes successfully, returns `run_id` |
| 2 | Query `usage_event` for LLM rows: `SELECT * FROM usage_event WHERE run_id = '<skill_run_id>' AND event_type = 'llm'` | One or more LLM rows returned |
| 3 | Verify `root_entity_type` field | `root_entity_type = 'skill'` for all rows |
| 4 | Verify `root_entity_id` field | `root_entity_id = '<skill_id>'` |
| 5 | Verify `entity_type` field (leaf entity) | `entity_type = 'skill'` |
| 6 | Verify `entity_version_id` field | `entity_version_id = '<version_id>'` |
| 7 | Verify `entity_name` field | `entity_name = 'test-standalone-skill'` |
| 8 | Verify tokens and cost | `input_tokens > 0`, `output_tokens > 0`, `cost_nano > 0` |

## Expected Final State

Standalone skill run generates `usage_event` rows with `root_entity_type='skill'` and `entity_type='skill'`, containing actual tokens and cost values.

## Pass/Fail Criteria

**Pass:**
- All LLM rows have `root_entity_type = 'skill'`
- All LLM rows have `entity_type = 'skill'`
- Skill ID, version ID, and name are correctly populated
- Tokens and cost values are non-zero and reflect actual LLM usage

**Fail:**
- `root_entity_type` is not `'skill'`
- Skill entity fields are empty or incorrect
- Tokens or cost values are zero
