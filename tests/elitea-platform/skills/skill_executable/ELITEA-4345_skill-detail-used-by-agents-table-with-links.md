---
id: ELITEA-4345
title: "Verify Skill Detail page displays Used By Agents table with links to agent detail pages"
priority: critical
type: functional
module: analytics-skills
status: ready
execution_type: manual
tags: [feat:skills, feat:analytics, feat:agents, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6929]
---

## Preconditions

- User is logged in to `{{base_url}}`
- Test skill is configured in at least 3 different agents
- Agents have executed the test skill at least once

## Test Data

| Field | Value |
|-------|-------|
| Test Skill | skill-multi-agent-use |
| Test Agents | agent-alpha, agent-beta, agent-gamma |
| Skill Detail URL | `{{base_url}}/settings/analytics?tab=skills&skill_id=<skill_id>` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Configure test skill in 3 agents: agent-alpha, agent-beta, agent-gamma | Skill added to agent configurations (via load_skill) |
| 2 | Execute each agent at least once, ensuring skill is invoked | All 3 agents executed, skill invoked in each |
| 3 | Navigate to Settings → Analytics → Skills tab | Skills analytics page loads |
| 4 | Search for test skill and click on skill name | Skill detail page opens |
| 5 | Scroll to "Used By Agents" section on detail page | "Used By Agents" section visible |
| 6 | Verify table displays all 3 agents: agent-alpha, agent-beta, agent-gamma | All 3 agents listed in table |
| 7 | Verify table includes columns: Agent Name, Uses (or Runs), Last Used, etc. | Table columns display relevant metrics per agent |
| 8 | Click on "agent-alpha" name/link in the table | Navigation to agent-alpha detail page in Analytics |
| 9 | Verify agent detail page loads with correct agent data | Agent-alpha analytics detail page displayed |
| 10 | Use browser back button to return to Skill detail page | Skill detail page restored |
| 11 | Click on "agent-beta" name/link in the table | Navigation to agent-beta detail page in Analytics |
| 12 | Verify agent detail page loads with correct agent data | Agent-beta analytics detail page displayed |
| 13 | Return to Skill detail page and verify "Agents Using" KPI card matches table count | "Agents Using" KPI = 3 (matches "Used By Agents" table row count) |

## Expected Final State

- "Used By Agents" table lists all agents using the skill
- Agent names are clickable links to agent detail pages
- Navigation to agent detail works correctly
- "Agents Using" KPI matches the count of agents in the table

## Pass/Fail Criteria

**Pass:**
- "Used By Agents" table displays all 3 agents
- Agent names are clickable links
- Clicking agent name navigates to correct agent detail page
- "Agents Using" KPI = 3 (matches table row count)
- No broken links or navigation errors

**Fail:**
- "Used By Agents" table missing or empty
- Agent names not clickable (no links)
- Clicking agent name fails or navigates to wrong page
- "Agents Using" KPI ≠ table row count
- Broken links or 404 errors
