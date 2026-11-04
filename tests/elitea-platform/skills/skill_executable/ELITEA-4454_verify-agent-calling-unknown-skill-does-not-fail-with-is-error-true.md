---
id: ELITEA-4454
title: "Verify agent calling unknown skill does not fail with is_error=true"
priority: medium
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
- Agent with skill loading capability exists
- Skill name `nonexistent-skill` does NOT exist

## Test Data

| Field | Value |
|-------|-------|
| Agent name | `test-agent-unknown-skill` |
| Unknown skill name | `nonexistent-skill` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Execute agent that calls `load_skill('nonexistent-skill')` | Agent run completes (may show skill not found in logs) |
| 2 | Query agent LLM rows: `SELECT * FROM usage_event WHERE run_id = '<agent_run_id>' AND event_type = 'llm'` | LLM rows exist with `is_error = false` |
| 3 | Query skill row: `SELECT * FROM usage_event WHERE run_id = '<agent_run_id>' AND event_type = 'skill'` | One skill row returned |
| 4 | Verify skill row `is_error` field | `is_error = false` |
| 5 | Verify skill row `meta` field | Contains `"outcome": "unknown_skill"` or `"outcome": "skill_not_found"` |
| 6 | Query agent error count: `SELECT COUNT(DISTINCT run_id) FROM usage_event WHERE root_entity_type = 'agent' AND root_entity_id = '<agent_id>' AND is_error = true` | Count does NOT include this run |

## Expected Final State

Agent run with unknown skill is NOT marked as error. Skill row has `is_error=false` with `meta.outcome='unknown_skill'`.

## Pass/Fail Criteria

**Pass:**
- Agent run completes without error flag
- All `usage_event` rows have `is_error = false`
- Skill row `meta` contains outcome indicator (`unknown_skill` or `skill_not_found`)
- Agent error KPIs do NOT increment

**Fail:**
- Agent run marked with `is_error = true`
- Unknown skill name causes agent run to fail
- Agent error rate increases due to unknown skill
