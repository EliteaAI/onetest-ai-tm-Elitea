---
id: ELITEA-4449
title: "Verify Skills Activity page shows zero cost increment for agent-loaded skills"
priority: critical
type: functional
module: analytics
status: ready
execution_type: manual
tags: [feat:skills, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6926]
---

## Preconditions

- User is logged in to `{{base_url}}`
- User has admin access to Analytics section
- Test skill exists and has been used by agents

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/settings/analytics?tab=skills` |
| Skill name | `test-skill-agent-loaded` |
| Agent name | `test-agent-using-skill` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to `{{base_url}}/app/settings/analytics?tab=skills` | Skills Activity page loads |
| 2 | Locate the test skill `test-skill-agent-loaded` in the table | Skill row is visible |
| 3 | Check the "AGENT & CHAT USES" column for the skill | Shows count > 0 (indicating skill was used in agent) |
| 4 | Check the "TOKENS" column for the skill | Shows `---` or `0` (no tokens attributed to skill) |
| 5 | Check the "COST" column for the skill | Shows `---` or `$0.00` (no cost attributed to skill) |
| 6 | Execute agent that uses the skill 3 more times | Agent runs complete successfully |
| 7 | Refresh Skills Activity page | "AGENT & CHAT USES" increments by 3 |
| 8 | Verify TOKENS and COST columns after refresh | Values remain `---` or `0` / `$0.00` |

## Expected Final State

Skills Activity page shows usage count for agent-loaded skills but displays zero tokens and zero cost.

## Pass/Fail Criteria

**Pass:**
- "AGENT & CHAT USES" column increments when agent uses skill
- "TOKENS" column shows `---` or `0` for agent-loaded skills
- "COST" column shows `---` or `$0.00` for agent-loaded skills
- Page correctly reflects that skill tokens/cost are attributed to the agent, not the skill

**Fail:**
- TOKENS or COST columns show non-zero values for agent-loaded skills
- Usage count does not increment
- Skills Activity page double-counts tokens/cost
