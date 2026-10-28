---
id: ELITEA-4189
title: "Verify skill with Auto model applies Auto routing logic during execution"
priority: critical
type: functional
module: skill-run-settings
status: draft
execution_type: manual
tags: [feat:skills, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6921]
---

## Preconditions

- User is logged in to `{{base_url}}`
- A skill with Auto model configured in run_settings exists
- Auto routing is enabled and configured for the project
- User has permission to run skills

## Test Data

| Field | Value |
|-------|-------|
| Skill model | Auto |
| Auto routing | Enabled |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to skill with Auto model saved | Skill details page opens |
| 2 | Verify "Run settings" shows "Auto" | Model: Auto |
| 3 | Run skill with a simple prompt (should route to lighter model) | Skill executes |
| 4 | Check API response → Verify model selected by Auto routing | Response shows a model selected automatically (e.g., GPT-4 Turbo or Claude Sonnet) |
| 5 | Run skill again with a complex/reasoning-heavy prompt | Skill executes |
| 6 | Check API response → Verify Auto selected a more capable model | Response shows a higher-tier model (e.g., Claude Opus) |
| 7 | Verify execution metadata includes Auto routing decision | Metadata indicates Auto selection applied |
| 8 | Navigate to Run History → Verify both runs show models selected by Auto | Run history displays actual models used |

## Expected Final State

- Skill execution uses Auto routing logic
- Different prompts route to appropriate models
- Execution metadata confirms Auto routing
- Run history shows actual models selected

## Pass/Fail Criteria

**Pass:**
- Auto routing is applied during execution
- Simple prompts route to lighter models
- Complex prompts route to capable models
- Execution respects Auto configuration

**Fail:**
- Auto routing not applied
- Same model used regardless of prompt complexity
- Execution falls back to project default without Auto logic
- No Auto routing metadata in response
