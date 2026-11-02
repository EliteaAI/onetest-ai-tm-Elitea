---
id: ELITEA-4340
title: "Verify standalone and in-agent skill runs are counted separately without double-counting"
priority: critical
type: functional
module: analytics-skills
status: ready
execution_type: manual
tags: [feat:skills, feat:analytics, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6929]
---

## Preconditions

- User is logged in to `{{base_url}}`
- Test skill exists and is configured in at least one agent
- Test skill has been executed both standalone and via agent

## Test Data

| Field | Value |
|-------|-------|
| Test Skill | skill-test-dual-usage |
| Test Agent | agent-using-skill-test |
| Analytics URL | `{{base_url}}/settings/analytics?tab=skills` |
| Standalone Runs | 3 executions |
| In-Agent Uses | 5 invocations via agent |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Execute test skill standalone 3 times via Skills page or API | 3 standalone runs completed successfully |
| 2 | Record run IDs or timestamps for standalone executions | Run IDs recorded |
| 3 | Execute test agent that uses the test skill 5 times | Agent runs completed, skill invoked 5 times within agent context |
| 4 | Navigate to Settings → Analytics → Skills tab | Skills analytics page loads |
| 5 | Search for test skill in Skill Activity table | Test skill found in table |
| 6 | Check "Runs" column value for test skill | "Runs" = 3 (standalone executions only) |
| 7 | Check "Agent & Chat Uses" column value for test skill | "Agent & Chat Uses" = 5 (in-agent invocations only) |
| 8 | Calculate total invocations: Runs + Agent & Chat Uses | Total = 3 + 5 = 8 distinct invocations |
| 9 | Click on test skill name to open detail view | Skill detail page opens |
| 10 | Verify KPI cards: "Runs" = 3, "Agent & Chat Uses" = 5 | KPI cards display correct values |
| 11 | Check "Trigger Source" breakdown | Shows separate counts: standalone runs vs load_skill/mention |
| 12 | Verify "Recent Runs" table lists only the 3 standalone runs (not in-agent uses) | Recent Runs shows 3 standalone runs with links |

## Expected Final State

- Standalone runs counted only in "Runs" column (3 runs)
- In-agent uses counted only in "Agent & Chat Uses" column (5 uses)
- Total invocations = 8, with no overlap or double-counting
- Trigger Source breakdown distinguishes standalone vs in-agent clearly

## Pass/Fail Criteria

**Pass:**
- "Runs" = 3 (standalone only)
- "Agent & Chat Uses" = 5 (in-agent only)
- No double-counting: total = 8 distinct invocations
- Trigger Source breakdown correctly separates standalone from in-agent
- Recent Runs table lists only standalone executions

**Fail:**
- "Runs" or "Agent & Chat Uses" include duplicated counts
- Total count is less than 8 (under-counting) or more than 8 (double-counting)
- Trigger Source breakdown shows incorrect split
- Recent Runs includes in-agent uses (should only show standalone runs)
