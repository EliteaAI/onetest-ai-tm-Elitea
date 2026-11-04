---
id: ELITEA-4455
title: "Verify deduplication when agent loads same skill multiple times in one run"
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
- Test skill is published

## Test Data

| Field | Value |
|-------|-------|
| Agent name | `test-agent-duplicate-skill` |
| Skill name | `test-skill-dedup` |
| Load attempts | Agent calls `load_skill('test-skill-dedup')` twice in one run |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Execute agent that calls `load_skill('test-skill-dedup')` twice within the same run | Agent run completes successfully |
| 2 | Query skill rows: `SELECT * FROM usage_event WHERE run_id = '<agent_run_id>' AND event_type = 'skill' AND entity_name = 'test-skill-dedup'` | Exactly one skill row returned |
| 3 | Verify skill row `tool_name` field | `tool_name = 'load_skill'` |
| 4 | Verify skill row `meta` field | Contains `"source": "load_skill"` and potentially `"outcome": "already_active"` for the second call |
| 5 | Query total skill rows for run: `SELECT COUNT(*) FROM usage_event WHERE run_id = '<agent_run_id>' AND event_type = 'skill'` | Count = 1 (deduplication applied) |

## Expected Final State

Only one `event_type='skill'` row is created per distinct skill, even if agent loads it multiple times. Deduplication prevents duplicate skill rows.

## Pass/Fail Criteria

**Pass:**
- Exactly one skill row exists for the duplicated skill name
- No duplicate skill rows created for same (run_id, skill_id, source)
- Deduplication logic works correctly

**Fail:**
- Multiple skill rows created for same skill in one run
- Deduplication not applied
- Second `load_skill` call creates duplicate row
