---
id: ELITEA-4179
title: "Verify validation error is displayed when selecting fixed model without model_ref"
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
- User has permission to create skills
- Test environment allows creating an invalid fixed selection scenario

## Test Data

| Field | Value |
|-------|-------|
| Skill name | `test-skill-invalid-model` |
| Model selection | Fixed (but missing model_ref) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Skills → Create new skill | Skill editor opens |
| 2 | Enter skill name and instructions | Fields populated |
| 3 | Expand "Run settings" accordion | Run settings section displays |
| 4 | Attempt to configure a fixed model selection without proper model_ref (this may require API manipulation or edge case scenario) | Invalid state created |
| 5 | Click "Save" | Save operation blocked |
| 6 | Observe validation error message | Error displayed: "A fixed model selection requires a valid model reference" or similar |
| 7 | Verify skill is not saved | Skill remains in edit state, no success notification |

## Expected Final State

- Skill is not saved with invalid run_settings
- Clear validation error message is displayed
- User is guided to fix the issue

## Pass/Fail Criteria

**Pass:**
- Validation error is displayed clearly
- Save operation is blocked
- Error message describes the issue accurately
- Skill is not saved with invalid configuration

**Fail:**
- No validation error shown
- Skill saved with invalid run_settings
- Error message is unclear or missing
- System allows invalid state
