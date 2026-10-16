---
id: ELITEA-3825
title: "Unpublish preserves skill attachments"
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
- User has editor/admin role with publish/unpublish permissions
- Test agent published with 3 attached Skills
- All Skills functional in published version

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Agent Name | "Unpublish Test Agent" |
| Skill 1 | "Alpha Skill" |
| Skill 2 | "Beta Skill" |
| Skill 3 | "Gamma Skill" |
| Published Version | "1.0.0" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open published agent "Unpublish Test Agent" | Agent loads; status shows "Published" |
| 2 | Verify SKILLS section shows 3/5 | All 3 Skills visible: Alpha, Beta, Gamma |
| 3 | Click ⋮ menu → **Unpublish** | Confirmation dialog appears |
| 4 | Confirm unpublish action | Toast: "Agent has been unpublished" |
| 5 | Verify agent status | Status changed to "Draft" or "Unpublished" |
| 6 | Verify SKILLS section | Still shows 3/5: Alpha, Beta, Gamma (unchanged) |
| 7 | Open each Skill card | Skill configurations intact |
| 8 | Navigate to Agent Hub | Hub loads |
| 9 | Search for "Unpublish Test Agent" | Agent NO longer appears in Hub |
| 10 | Return to Agents menu | Agents list |
| 11 | Verify agent still exists in project | Agent visible in private project list |

## Expected Final State

Unpublishing does NOT affect draft/source agent's Skill attachments. All Skills remain intact and functional in source project. Agent is removed from Agent Hub.

## Pass/Fail Criteria

**Pass:**
- Unpublishing does NOT affect draft/source agent's Skill attachments
- All Skills remain intact and functional in source project
- Agent removed from Agent Hub after unpublish
- Agent still accessible in private project

**Fail:**
- Skills removed or modified during unpublish
- Agent still appears in Agent Hub
- Skills broken after unpublish
