---
id: ELITEA-4174
title: "Verify fixed model with reasoning level and max tokens persists after save and reload"
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
- User has permission to create skills (`models.applications.skills.create`)
- At least one reasoning model is available in the project

## Test Data

| Field | Value |
|-------|-------|
| Skill name | `test-skill-fixed-model` |
| Model | GPT-4 Turbo (or any available reasoning model) |
| Reasoning level | Medium (for 3-point scale) or High (for 5-point scale) |
| Max tokens | 5000 |
| Project context | ON (default) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Skills section → Click "Create Skill" | Skill editor opens |
| 2 | Enter skill name and instructions | Fields populated |
| 3 | Expand "Run settings" accordion | Run settings section displays |
| 4 | Click on Model selector → Select a fixed reasoning model (e.g., GPT-4 Turbo) | Model selected |
| 5 | Click settings icon next to model → Model settings dialog opens | Dialog shows REASONING slider and MAX COMPLETION TOKENS section |
| 6 | Set REASONING slider to "Medium" (3-point) or "High" (5-point depending on model) | Slider position updated |
| 7 | Select "Custom" for Max Completion Tokens → Enter 5000 | Max tokens set to 5000 |
| 8 | Click "Apply" | Settings saved, dialog closes |
| 9 | Click "Save" button | Skill saved successfully, success notification displayed |
| 10 | Navigate away from the skill (go to Skills list) | Skills list displayed |
| 11 | Navigate back to the skill details page | Skill details displayed |
| 12 | Expand "Run settings" accordion | Run settings section displays |
| 13 | Verify Model field shows the previously selected model | Model persisted correctly |
| 14 | Click settings icon next to model → Verify REASONING level | Reasoning level shows "Medium" or "High" (as set in step 6) |
| 15 | Verify Max tokens shows 5000 | Max tokens persisted correctly |

## Expected Final State

- Skill is saved with run_settings containing: fixed model, reasoning level, and max_tokens
- All settings persist after page reload
- Run settings section displays saved values correctly

## Pass/Fail Criteria

**Pass:**
- Model selection persists after reload
- Reasoning level persists at the configured value (Medium or High)
- Max tokens persists at 5000
- No data loss or default override occurs

**Fail:**
- Model reverts to default or null after reload
- Reasoning level resets to default
- Max tokens resets to default
- Any run_settings field is lost
