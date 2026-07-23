---
id: ELITEA-2236
title: "Standalone skill publish does NOT affect agent's embedded copy"
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
- Agent published with attached Skills (including draft-only Skill)
- Skills Studio accessible

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Agent Name | "Independence Test Agent" |
| Skill | "Draft Skill" - embedded in agent, currently draft-only in Skills Studio |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Verify agent published with Skills | Agent in Agent Hub |
| 2 | Add agent to conversation | Agent ready |
| 3 | Test "Draft Skill" functionality | Works (embedded in agent snapshot) |
| 4 | Note the Skill behavior | Record specific behavior |
| 5 | Navigate to Skills Studio | Skills list |
| 6 | Open "Draft Skill" | Skill editor |
| 7 | Standalone-publish "Draft Skill" via Skills Studio | Skill now published in Skills Studio |
| 8 | Return to conversation with published agent | Same conversation |
| 9 | Test "Draft Skill" functionality again | Behavior UNCHANGED |
| 10 | Standalone-unpublish "Draft Skill" in Skills Studio | Skill back to draft |
| 11 | Test agent's embedded Skill again | Still works (snapshot isolated) |

## Expected Final State

Standalone-publishing or unpublishing a Skill does NOT affect the embedded copy in a previously published agent. Agent's embedded Skill snapshot is isolated from standalone Skill status.

## Pass/Fail Criteria

**Pass:**
- Standalone-publishing a Skill does NOT affect agent's embedded copy
- Standalone-unpublishing a Skill does NOT break agent's embedded copy
- Agent's embedded Skill snapshot is isolated from standalone Skill status

**Fail:**
- Standalone publish/unpublish affects agent's embedded Skill
- Agent Skill behavior changes without re-publishing agent
