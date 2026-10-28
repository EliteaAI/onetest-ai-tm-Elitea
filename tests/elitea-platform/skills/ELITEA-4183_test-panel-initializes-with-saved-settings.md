---
id: ELITEA-4183
title: "Verify Test Panel initializes with saved model and settings from run_settings"
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
- A skill with configured run_settings exists (fixed model, reasoning level, max tokens)

## Test Data

| Field | Value |
|-------|-------|
| Skill | Skill with run_settings configured |
| Saved model | GPT-4 Turbo |
| Saved reasoning | High |
| Saved max tokens | 8000 |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to skill with configured run_settings | Skill details page opens |
| 2 | Click "Test" tab or open Test Panel | Test Panel opens |
| 3 | Observe Model selector in Test Panel | Model dropdown displays the saved model (GPT-4 Turbo) as pre-selected |
| 4 | Click Model settings icon in Test Panel | Settings dialog opens |
| 5 | Verify REASONING slider shows "High" (matching saved setting) | Reasoning level: High |
| 6 | Verify Max tokens shows 8000 (matching saved setting) | Max tokens: 8000 |
| 7 | Close settings → Verify Test Panel is ready with saved configuration | Test Panel initialized with saved settings |
| 8 | Enter a test prompt → Click "Run" → Observe execution | Skill executes using the saved model and settings |

## Expected Final State

- Test Panel starts with saved run_settings as defaults
- User can override settings in Test Panel (local state)
- Test execution uses the model and settings displayed in Test Panel

## Pass/Fail Criteria

**Pass:**
- Test Panel initializes with saved model
- Reasoning level matches saved setting
- Max tokens matches saved setting
- Test execution uses correct configuration

**Fail:**
- Test Panel starts with project default instead of saved settings
- Reasoning level or max tokens do not match saved values
- Test Panel ignores run_settings
- Execution uses incorrect model
