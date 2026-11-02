---
id: ELITEA-4341
title: "Verify in-agent skill uses display zero cost and zero tokens by design"
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
- Test skill is configured in test agent and has been invoked via agent
- Skill has no standalone runs (only in-agent uses)

## Test Data

| Field | Value |
|-------|-------|
| Test Skill | skill-in-agent-only |
| Test Agent | agent-with-skill-in-agent-only |
| Analytics URL | `{{base_url}}/settings/analytics?tab=skills` |
| In-Agent Uses | 10 invocations via agent |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Execute test agent 10 times, ensuring test skill is invoked each time | Agent runs completed, skill invoked 10 times in-agent |
| 2 | Verify agent run analytics show cost and tokens for the agent run | Agent analytics display non-zero cost and tokens (attributed to agent/skill-root) |
| 3 | Navigate to Settings → Analytics → Skills tab | Skills analytics page loads |
| 4 | Search for test skill (skill-in-agent-only) in Skill Activity table | Test skill found in table |
| 5 | Check "Runs" column value | "Runs" = 0 or "—" (no standalone runs) |
| 6 | Check "Agent & Chat Uses" column value | "Agent & Chat Uses" = 10 |
| 7 | Check "Tokens" column value | "Tokens" = 0 or "—" (in-agent uses carry no tokens) |
| 8 | Check "Cost" column value | "Cost" = $0.00 or "—" (in-agent uses carry no cost) |
| 9 | Click on test skill name to open detail view | Skill detail page opens |
| 10 | Verify KPI cards: "Tokens" = 0 or "—", "Cost" = $0.00 or "—" | KPI cards show zero tokens and zero cost |
| 11 | Check tooltip or help text explaining why tokens/cost are zero for in-agent uses | Tooltip explains: "In-agent uses show $0 cost as cost is attributed to the skill-root/agent" |
| 12 | Navigate to Analytics → Guide tab and find Skills section | Guide explains in-agent uses have zero cost/tokens by design |

## Expected Final State

- In-agent uses show "Agent & Chat Uses" = 10
- Tokens and Cost for in-agent-only skill = 0 or "—"
- Tooltip or Guide explains cost attribution to skill-root/agent
- No cost/tokens incorrectly attributed to in-agent uses

## Pass/Fail Criteria

**Pass:**
- "Agent & Chat Uses" = 10
- "Tokens" = 0 or "—" for in-agent-only skill
- "Cost" = $0.00 or "—" for in-agent-only skill
- Tooltip or Guide clearly explains zero cost/tokens by design
- Cost and tokens correctly attributed to agent/skill-root, not to in-agent uses

**Fail:**
- "Tokens" or "Cost" show non-zero values for in-agent uses
- No explanation provided for zero cost/tokens
- Confusion between standalone cost/tokens vs in-agent (zero by design)
