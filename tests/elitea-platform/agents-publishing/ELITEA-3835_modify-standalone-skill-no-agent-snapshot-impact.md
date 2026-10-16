---
id: ELITEA-3835
title: "Modify standalone skill does NOT affect agent's snapshot"
priority: high
type: functional
module: agents-publishing
status: draft
execution_type: manual
tags: [feat:skills, feat:agent-publishing, r-2.0.5]
requirements: [EliteaAI/elitea_issues#5803]
---

## Preconditions

- User is logged in to `{{base_url}}`
- User has editor/admin role with publish permissions
- Agent published with a Skill that is also standalone-published
- Skills Studio accessible

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Agent Name | "Independence Test Agent" |
| Skill | "Published Skill" - both embedded in agent AND standalone-published |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Skills Studio | Skills list |
| 2 | Open "Published Skill" | Skill editor |
| 3 | Modify Skill content significantly | Change instructions (e.g., add new directive) |
| 4 | Save and re-publish standalone Skill | Skill updated in Skills Studio |
| 5 | Navigate to Agent Hub | Hub loads |
| 6 | Find published "Independence Test Agent" | Agent card visible |
| 7 | Add to conversation | Agent ready |
| 8 | Test "Published Skill" functionality | Uses ORIGINAL content from agent publish time |
| 9 | Verify snapshot isolation | Agent's embedded Skill NOT affected by standalone update |
| 10 | To get new Skill content | Would require re-publishing the agent |

## Expected Final State

Modifying and re-publishing a standalone Skill does NOT update the embedded copy in a previously published agent. Agent's embedded Skill uses content from agent publish time. The two publishing mechanisms are completely independent.

## Pass/Fail Criteria

**Pass:**
- Modifying standalone-published Skill does NOT update agent's snapshot
- Agent's embedded Skill uses content from agent publish time
- Two publishing mechanisms are completely independent and isolated

**Fail:**
- Standalone Skill modification affects agent's embedded copy
- Agent uses updated Skill content without re-publishing
