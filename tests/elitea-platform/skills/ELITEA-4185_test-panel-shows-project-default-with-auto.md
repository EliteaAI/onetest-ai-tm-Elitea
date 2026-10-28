---
id: ELITEA-4185
title: "Verify Test Panel displays project default model when skill is saved with Auto selection"
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
- Auto model selection is enabled for the project
- A skill with Auto model is saved
- Project has a default model configured (e.g., GPT-4 Turbo)

## Test Data

| Field | Value |
|-------|-------|
| Skill model | Auto |
| Project default | GPT-4 Turbo |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to skill with Auto model saved | Skill details page opens |
| 2 | Expand "Run settings" → Verify Model shows "Auto" | Model: Auto |
| 3 | Click "Test" tab or open Test Panel | Test Panel opens |
| 4 | Observe Model selector in Test Panel | Model dropdown shows project default (GPT-4 Turbo), NOT "Auto" option |
| 5 | Verify "Auto" is NOT listed in Test Panel model dropdown | Auto option not available in Test Panel |
| 6 | Verify helper text explains stateless Test Panel uses concrete model | Helper text: "Test Panel requires a specific model (Auto not supported)" or similar |
| 7 | Change model in Test Panel to a different model (e.g., Claude Sonnet) → Run test | Test executes with selected model |
| 8 | Return to skill editor → Verify saved model is still "Auto" (Test Panel change is local) | Saved run_settings unchanged |

## Expected Final State

- Test Panel cannot use Auto (requires concrete model)
- Test Panel starts with project default when skill uses Auto
- Saved run_settings remain Auto (Test Panel changes are local only)
- User can override model in Test Panel

## Pass/Fail Criteria

**Pass:**
- Test Panel shows project default when skill uses Auto
- Auto option not available in Test Panel dropdown
- Test Panel model selection is independent of saved run_settings
- Saved run_settings remain Auto after Test Panel usage

**Fail:**
- Test Panel attempts to use Auto
- Test Panel shows Auto option in dropdown
- Test Panel fails to load when skill uses Auto
- Changing model in Test Panel modifies saved run_settings
