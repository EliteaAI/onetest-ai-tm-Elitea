---
id: ELITEA-3829
title: "Verify agent uses its own model when running attached skill, ignoring skill's run_settings"
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
- A skill with run_settings configured exists (Model: Claude Opus, Reasoning: High)
- An agent with different model exists (Model: GPT-4 Turbo)
- Skill is attached to the agent
- User has permission to run agents

## Test Data

| Entity | Model | Reasoning | Context |
|--------|-------|-----------|---------|
| Skill | Claude Opus | High | OFF |
| Agent | GPT-4 Turbo | Medium | ON |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to agent details page | Agent page opens |
| 2 | Verify agent's model is GPT-4 Turbo with Reasoning: Medium | Agent model: GPT-4 Turbo, Reasoning: Medium |
| 3 | Verify skill is attached in agent's configuration | Skill listed in attached skills |
| 4 | Open attached skill details (in new tab) → Verify skill's run_settings show Claude Opus, Reasoning: High | Skill model: Claude Opus, Reasoning: High |
| 5 | Return to agent → Start agent conversation | Agent chat opens |
| 6 | Send prompt that invokes the attached skill (e.g., "~skill-name help me with...") | Skill invoked within agent context |
| 7 | Wait for response | Agent completes execution |
| 8 | Check API response or execution logs → Verify model used is GPT-4 Turbo (agent's model), NOT Claude Opus (skill's model) | Model used: GPT-4 Turbo |
| 9 | Verify reasoning effort is Medium (agent's setting), NOT High (skill's setting) | Reasoning: Medium |
| 10 | Verify project context is ON (agent's setting), NOT OFF (skill's setting) | Context: ON |
| 11 | Navigate to Run History → Verify agent run shows agent's model, not skill's | Run history: GPT-4 Turbo |

## Expected Final State

- Agent uses its own model and settings when executing attached skill
- Skill's run_settings are ignored during agent execution
- Agent's LLM configuration takes precedence
- Agent behavior is unchanged from before this feature

## Pass/Fail Criteria

**Pass:**
- Agent uses its own model (GPT-4 Turbo), not skill's (Claude Opus)
- Agent uses its own reasoning level (Medium), not skill's (High)
- Agent respects its own context setting (ON), not skill's (OFF)
- Skill's run_settings have no effect on agent execution

**Fail:**
- Agent uses skill's model instead of its own
- Agent's model or settings are overridden by skill's run_settings
- Context setting from skill affects agent
- Agent behavior changed due to skill's run_settings
