---
id: ELITEA-4448
title: "Verify agent total cost remains unchanged when loading multiple skills"
priority: critical
type: regression
module: usage-metering
status: ready
execution_type: manual
tags: [feat:skills, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6926]
---

## Preconditions

- User is logged in to `{{base_url}}`
- Database access to `usage_event` table
- Agent configured with capability to load skills
- Three test skills are published: `skill-1`, `skill-2`, `skill-3`

## Test Data

| Field | Value |
|-------|-------|
| Agent name | `test-agent-multi-skill` |
| Skills to load | `skill-1`, `skill-2`, `skill-3` |
| Baseline run | Agent run WITHOUT loading any skills |
| Test run | Agent run WITH 3 skills loaded |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Execute agent WITHOUT loading any skills, record `run_id_baseline` | Agent completes successfully |
| 2 | Query total cost: `SELECT SUM(cost_nano) FROM usage_event WHERE run_id = '<run_id_baseline>' AND event_type = 'llm'` | Record baseline cost value (e.g., `cost_baseline`) |
| 3 | Execute same agent WITH 3 skills loaded via `load_skill`, record `run_id_test` | Agent completes successfully |
| 4 | Query total cost: `SELECT SUM(cost_nano) FROM usage_event WHERE run_id = '<run_id_test>' AND event_type = 'llm'` | Record test cost value (e.g., `cost_test`) |
| 5 | Compare costs: `cost_baseline` vs `cost_test` | Values are identical (difference ≤ 1% due to potential LLM variance) |
| 6 | Verify skill rows: `SELECT COUNT(*) FROM usage_event WHERE run_id = '<run_id_test>' AND event_type = 'skill'` | Exactly 3 skill rows exist |
| 7 | Verify skill rows cost: `SELECT SUM(cost_nano) FROM usage_event WHERE run_id = '<run_id_test>' AND event_type = 'skill'` | Sum = 0 |

## Expected Final State

Agent total cost (LLM events only) is identical with or without skills loaded. Skill rows contribute zero cost.

## Pass/Fail Criteria

**Pass:**
- Baseline and test agent total costs are identical (within 1% margin)
- Exactly 3 `event_type='skill'` rows created
- Sum of skill row costs = 0

**Fail:**
- Agent cost increases when skills are loaded
- Skill rows contribute non-zero cost to agent total
- Wrong number of skill rows created
