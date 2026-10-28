---
id: ELITEA-4188
title: "Verify skill with fixed model uses the configured model during execution"
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
- A skill with fixed model configured in run_settings exists (e.g., Claude Opus)
- Project default model is different (e.g., GPT-4 Turbo)
- User has permission to run skills

## Test Data

| Field | Value |
|-------|-------|
| Skill model | Claude Opus (fixed) |
| Project default | GPT-4 Turbo |
| Reasoning level | Medium |
| Max tokens | 6000 |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to skill with fixed model (Claude Opus) | Skill details page opens |
| 2 | Verify "Run settings" shows Claude Opus | Model: Claude Opus |
| 3 | Click "Run" button or execute skill via API | Skill execution starts |
| 4 | Wait for execution to complete | Skill run completes successfully |
| 5 | Check API response or execution metadata for model used | Response contains `model: "claude-opus-4.5"` or similar |
| 6 | Verify execution did NOT use project default (GPT-4 Turbo) | Model used is Claude Opus, NOT project default |
| 7 | Check token usage or logs → Verify reasoning level and max tokens applied | Reasoning: Medium, Max tokens: 6000 applied |
| 8 | Navigate to Run History → Verify run record shows correct model | Run history displays Claude Opus as model used |

## Expected Final State

- Skill execution uses the configured fixed model from run_settings
- Project default model is ignored
- Reasoning level and max tokens from run_settings are applied
- Execution metadata reflects correct configuration

## Pass/Fail Criteria

**Pass:**
- Skill executes with Claude Opus (not project default)
- API response confirms correct model used
- Reasoning and token settings applied correctly
- Run history shows correct model

**Fail:**
- Skill uses project default instead of saved model
- API response shows incorrect model
- Reasoning or token settings not applied
- Execution ignores run_settings
