---
id: ELITEA-4180
title: "Verify permission error is displayed when configuring a model from another project without access"
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
- User is in Project A
- A model exists in Project B that the user does NOT have access to
- User has permission to create skills in Project A

## Test Data

| Field | Value |
|-------|-------|
| Current project | Project A |
| Model | Model from Project B (no access) |
| Skill name | `test-skill-cross-project` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Skills in Project A → Create new skill | Skill editor opens |
| 2 | Enter skill name and instructions | Fields populated |
| 3 | Expand "Run settings" accordion | Run settings section displays |
| 4 | Attempt to select or configure a model from Project B (may require API manipulation or specific test setup) | Model selection attempted |
| 5 | Click "Save" | Save operation blocked |
| 6 | Observe error message | Permission error displayed: "You do not have access to the selected model" or similar |
| 7 | Verify skill is not saved | Skill remains in draft, no success notification |

## Expected Final State

- Skill is not saved with unauthorized model
- Clear permission error message displayed
- User is informed about access restriction

## Pass/Fail Criteria

**Pass:**
- Permission error is displayed
- Save operation is blocked
- Error message clearly indicates permission issue
- Skill is not saved with unauthorized model

**Fail:**
- No permission error shown
- Skill saved with model user cannot access
- Error message is unclear
- System allows unauthorized access
