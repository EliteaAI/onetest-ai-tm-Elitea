---
id: ELITEA-4193
title: "Verify agent with attached skill maintains unchanged available_skills registry and load_skill tool behavior"
priority: critical
type: regression
module: skill-run-settings
status: draft
execution_type: manual
tags: [feat:skills, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6921]
---

## Preconditions

- User is logged in to `{{base_url}}`
- An agent with multiple attached skills exists
- At least one skill has run_settings configured
- User has permission to run agents and view system prompts

## Test Data

| Field | Value |
|-------|-------|
| Agent | Agent with 3 attached skills |
| Skill 1 | Skill with run_settings |
| Skill 2 | Skill without run_settings (legacy) |
| Skill 3 | Skill with run_settings |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to agent details page | Agent page opens |
| 2 | Verify 3 skills are attached | 3 skills listed |
| 3 | Start agent conversation | Agent chat opens |
| 4 | Inspect system prompt (via API or debug tools) → Check `<available_skills>` registry | Registry contains all 3 skills with name + description only |
| 5 | Verify registry does NOT include skill run_settings (model, reasoning, context) | Run_settings not exposed in registry |
| 6 | Verify registry format is unchanged from before run_settings feature | Registry matches legacy format |
| 7 | Send prompt that invokes a skill using `~skill-name` syntax | Skill invoked successfully |
| 8 | Verify `load_skill` meta-tool behavior is unchanged | Skill loads correctly, same behavior as before |
| 9 | Verify explicit `~skill-name` invocation works correctly | Skill executes within agent context |
| 10 | Send prompt that should NOT trigger skill → Verify agent responds normally | Agent responds without invoking skills |
| 11 | Check prompt cache stability → Verify registry size unchanged | Cache hit rate maintained, no registry bloat |

## Expected Final State

- `<available_skills>` registry format unchanged
- Registry contains name + description only (no run_settings)
- `load_skill` meta-tool behavior unchanged
- Progressive disclosure and explicit invocation work as before
- Prompt cache stability maintained

## Pass/Fail Criteria

**Pass:**
- Available_skills registry format is identical to pre-feature format
- Run_settings not exposed in registry
- load_skill tool behavior unchanged
- Skill invocation mechanisms work as before
- No regression in agent-skill integration

**Fail:**
- Registry includes run_settings fields
- Registry format changed
- load_skill behavior modified
- Skill invocation broken or changed
- Prompt cache degraded
