---
id: ELITEA-4451
title: "Verify agent is root entity and skill is leaf entity when agent loads skill"
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
- Agent with skill loading capability exists
- Test skill is published

## Test Data

| Field | Value |
|-------|-------|
| Agent name | `test-agent` |
| Agent ID | `<agent_id>` |
| Skill name | `test-skill` |
| Skill ID | `<skill_id>` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Execute agent that calls `load_skill('test-skill')` | Agent run completes successfully, returns `run_id` |
| 2 | Query agent LLM rows: `SELECT * FROM usage_event WHERE run_id = '<agent_run_id>' AND event_type = 'llm'` | One or more LLM rows returned |
| 3 | Verify root entity for LLM rows | `root_entity_type = 'agent'`, `root_entity_id = '<agent_id>'` |
| 4 | Verify leaf entity for LLM rows | `entity_type = 'agent'`, `entity_id = '<agent_id>'` |
| 5 | Query skill row: `SELECT * FROM usage_event WHERE run_id = '<agent_run_id>' AND event_type = 'skill'` | Exactly one skill row returned |
| 6 | Verify root entity for skill row | `root_entity_type = 'agent'`, `root_entity_id = '<agent_id>'` |
| 7 | Verify leaf entity for skill row | `entity_type = 'skill'`, `entity_id = '<skill_id>'`, `entity_name = 'test-skill'` |
| 8 | Verify skill row has zero cost | `cost_nano = 0`, all token fields = 0 |

## Expected Final State

Agent LLM rows have `root_entity_type='agent'` and `entity_type='agent'`. Skill row has `root_entity_type='agent'` but `entity_type='skill'` (leaf entity).

## Pass/Fail Criteria

**Pass:**
- Agent LLM rows: `root_entity_type = 'agent'` and `entity_type = 'agent'`
- Skill row: `root_entity_type = 'agent'` and `entity_type = 'skill'`
- Skill row has zero tokens and zero cost
- Entity IDs and names are correctly populated

**Fail:**
- Root entity type is incorrect for any row
- Skill is attributed as root entity when loaded by agent
- Entity type attribution is mixed or incorrect
