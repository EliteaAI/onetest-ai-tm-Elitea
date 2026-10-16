---
id: ELITEA-3831
title: "Agent publish does NOT create standalone skill entities"
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
- Test agent with Skills attached
- Agent Hub accessible

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Agent Name | "Independence Test Agent" |
| Skill 1 | "Helper Skill" - valid instructions (100+ chars) |
| Skill 2 | "Guide Skill" - valid instructions (100+ chars) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open "Independence Test Agent" with 2 Skills attached | Agent loads with Skills visible |
| 2 | Click ⋮ menu → **Publish** | Publish wizard opens |
| 3 | Complete full publish flow | Agent published successfully |
| 4 | Navigate to **Agent Hub** | Agent Hub page loads |
| 5 | Search for "Independence Test Agent" | Published agent appears as card |
| 6 | Search for "Helper Skill" | **No standalone Skill entity appears** |
| 7 | Search for "Guide Skill" | **No standalone Skill entity appears** |
| 8 | Browse Agent Hub categories | No Skill entries visible as independent items |

## Expected Final State

Publishing an agent does NOT create standalone Skill entries in Agent Hub. Skills remain embedded in agent snapshot and are not exposed as separate entities.

## Pass/Fail Criteria

**Pass:**
- Publishing agent does NOT create standalone Skill entries in Agent Hub
- Skills remain embedded in agent snapshot, not exposed as separate entities
- Only the parent agent is discoverable in Agent Hub

**Fail:**
- Skills appear as independent entities in Agent Hub
- Skills discoverable separately from agent
