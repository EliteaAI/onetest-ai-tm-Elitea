---
id: ELITEA-4453
title: "Verify standalone skill runs do not increment agent run count in KPIs"
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
- User has admin access to Analytics section
- Database access to `usage_event` table
- Test skill published for standalone execution

## Test Data

| Field | Value |
|-------|-------|
| Skill name | `test-standalone-skill` |
| Number of skill runs | 5 standalone executions |
| Analytics URL | `{{base_url}}/app/settings/analytics?tab=agents` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to `{{base_url}}/app/settings/analytics?tab=agents` | Agents & Pipelines analytics page loads |
| 2 | Record baseline "Most Active Agents & Pipelines" run count | Record `baseline_agent_runs` |
| 3 | Execute test skill standalone 5 times via S1 API | All 5 skill runs complete successfully |
| 4 | Verify skill runs in database: `SELECT COUNT(DISTINCT run_id) FROM usage_event WHERE root_entity_type = 'skill'` | Count includes 5 new skill runs |
| 5 | Refresh Agents & Pipelines analytics page | Page reloads with updated data |
| 6 | Check "Most Active Agents & Pipelines" run count | Count remains `baseline_agent_runs` (unchanged) |
| 7 | Query agent run count expression: `SELECT COUNT(DISTINCT run_id) FROM usage_event WHERE root_entity_type IN ('agent', 'pipeline')` | Count does NOT include the 5 skill runs |
| 8 | Navigate to Skills Activity tab | Skills Activity page loads |
| 9 | Verify skill run count shows 5 new runs | Skill shows 5 runs in Skills Activity |

## Expected Final State

Standalone skill runs are tracked separately in Skills Activity page but do NOT increment agent run counts in Agents & Pipelines analytics.

## Pass/Fail Criteria

**Pass:**
- Agent run count in Agents & Pipelines analytics remains unchanged after standalone skill executions
- Skill runs are counted only in Skills Activity page
- Database query for `root_entity_type IN ('agent', 'pipeline')` excludes skill runs
- Skills Activity page correctly shows skill run count

**Fail:**
- Agent run count increases when standalone skills are executed
- Skill runs are mixed with agent runs in KPIs
- Skills Activity page does not show skill runs
