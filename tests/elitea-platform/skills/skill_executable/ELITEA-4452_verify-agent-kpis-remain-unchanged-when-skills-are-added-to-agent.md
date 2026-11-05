---
id: ELITEA-4452
title: "Verify agent KPIs remain unchanged when skills are added to agent"
priority: high
type: regression
module: analytics
status: ready
execution_type: manual
tags: [feat:skills, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6926]
---

## Preconditions

- User is logged in to `{{base_url}}`
- Database access to `usage_event` table
- Baseline agent exists WITHOUT skill loading
- Test agent exists WITH skill loading capability
- Both agents perform identical LLM operations

## Test Data

| Field | Value |
|-------|-------|
| Baseline agent | `baseline-agent-no-skills` |
| Test agent | `test-agent-with-skills` |
| Number of skills | 3 skills loaded |
| Number of runs | 5 runs each |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Execute baseline agent 5 times (no skill loading) | 5 successful runs |
| 2 | Query agent run count: `SELECT COUNT(DISTINCT run_id) FROM usage_event WHERE root_entity_type = 'agent' AND root_entity_id = '<baseline_agent_id>'` | Count = 5 |
| 3 | Query total tokens: `SELECT SUM(input_tokens + output_tokens) FROM usage_event WHERE root_entity_type = 'agent' AND root_entity_id = '<baseline_agent_id>' AND event_type = 'llm'` | Record `baseline_tokens` |
| 4 | Query total cost: `SELECT SUM(cost_nano) FROM usage_event WHERE root_entity_type = 'agent' AND root_entity_id = '<baseline_agent_id>' AND event_type = 'llm'` | Record `baseline_cost` |
| 5 | Execute test agent 5 times (with 3 skills loaded each run) | 5 successful runs |
| 6 | Query agent run count for test agent | Count = 5 (same as baseline) |
| 7 | Query total tokens for test agent | `test_tokens` ≈ `baseline_tokens` (within 5% variance) |
| 8 | Query total cost for test agent | `test_cost` ≈ `baseline_cost` (within 5% variance) |
| 9 | Query skill rows: `SELECT COUNT(*) FROM usage_event WHERE root_entity_type = 'agent' AND root_entity_id = '<test_agent_id>' AND event_type = 'skill'` | Count = 15 (3 skills × 5 runs) |
| 10 | Verify skill rows contribute zero cost: `SELECT SUM(cost_nano) FROM usage_event WHERE event_type = 'skill' AND root_entity_id = '<test_agent_id>'` | Sum = 0 |

## Expected Final State

Agent run counts, token totals, and cost totals remain unchanged when skills are loaded. Skill rows exist but contribute zero to agent KPIs.

## Pass/Fail Criteria

**Pass:**
- Agent run counts are identical (baseline = test)
- Token totals are identical within 5% variance
- Cost totals are identical within 5% variance
- Skill rows exist but have zero tokens and zero cost

**Fail:**
- Agent run count changes when skills added
- Token or cost totals increase significantly (>5%)
- Skill rows contribute non-zero cost to agent totals
