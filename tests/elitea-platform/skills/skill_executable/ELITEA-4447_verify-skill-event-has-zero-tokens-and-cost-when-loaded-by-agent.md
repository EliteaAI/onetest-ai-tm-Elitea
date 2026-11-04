---
id: ELITEA-4447
title: "Verify skill event has zero tokens and cost when loaded by agent"
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
- Agent with `load_skill` capability exists
- Test skill is published and available

## Test Data

| Field | Value |
|-------|-------|
| Agent name | `test-agent-with-skill` |
| Skill name | `test-skill` |
| API endpoint | `{{base_url}}/api/v1/agents/run` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Execute agent that calls `load_skill('test-skill')` via API | Agent run completes successfully |
| 2 | Query `usage_event` table: `SELECT * FROM usage_event WHERE run_id = '<agent_run_id>' AND event_type = 'skill'` | One row returned with `entity_name = 'test-skill'` |
| 3 | Verify token fields in the skill row | `input_tokens = 0`, `output_tokens = 0`, `cache_read_tokens = 0`, `cache_creation_tokens = 0` |
| 4 | Verify cost field in the skill row | `cost_nano = 0` and `cost_usd = 0.00` |
| 5 | Verify error status | `is_error = false` |

## Expected Final State

`usage_event` table contains one `event_type='skill'` row with all token and cost fields set to zero, while agent LLM rows contain the actual tokens/cost.

## Pass/Fail Criteria

**Pass:**
- Skill row exists with `event_type='skill'`
- All token fields (`input_tokens`, `output_tokens`, `cache_read_tokens`, `cache_creation_tokens`) = 0
- `cost_nano = 0` and `cost_usd = 0.00`
- `is_error = false`

**Fail:**
- Skill row has any non-zero token count
- Skill row has any non-zero cost value
- No skill row created when agent loads skill
