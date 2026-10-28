---
id: ELITEA-4176
title: "Verify 'Include project context' toggle OFF persists after save and reload"
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
- A project with project context is available

## Test Data

| Field | Value |
|-------|-------|
| Skill name | `test-skill-no-context` |
| Model | Any available model |
| Project context toggle | OFF |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Skills → Create new skill | Skill editor opens |
| 2 | Enter skill name and instructions | Fields populated |
| 3 | Expand "Run settings" accordion | Run settings section displays |
| 4 | Verify "Include project context" toggle is ON by default | Toggle shows enabled state |
| 5 | Click "Include project context" toggle to turn it OFF | Toggle changes to disabled state, helper text may update |
| 6 | Click "Save" | Skill saved successfully |
| 7 | Navigate away and return to the skill | Skill details page reloads |
| 8 | Expand "Run settings" accordion | Run settings section displays |
| 9 | Verify "Include project context" toggle is OFF | Toggle shows disabled state |

## Expected Final State

- Skill saved with run_settings.ignore_project_context = true
- Toggle state persists after reload
- Project context will be excluded during skill execution

## Pass/Fail Criteria

**Pass:**
- Toggle state OFF is saved correctly
- Toggle state persists after reload showing OFF
- run_settings contains ignore_project_context = true

**Fail:**
- Toggle reverts to ON after reload
- Setting is not saved
- Toggle state is inconsistent with saved data
