---
id: ELITEA-4175
title: "Verify Auto model selection persists after save and reload"
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
- Auto model selection is enabled for the project
- Project has Auto routing configured

## Test Data

| Field | Value |
|-------|-------|
| Skill name | `test-skill-auto-model` |
| Model selection | Auto |
| Project context | ON |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Skills → Click "Create Skill" | Skill editor opens |
| 2 | Enter skill name and instructions | Fields populated |
| 3 | Expand "Run settings" accordion | Run settings section displays |
| 4 | Click on Model selector → Verify "Auto" option is available | Auto option listed in dropdown |
| 5 | Select "Auto" | Auto model selected |
| 6 | Verify helper text explains Auto behavior | Helper text: "Model will be automatically selected based on task complexity" or similar |
| 7 | Click "Save" | Skill saved successfully |
| 8 | Reload the page (F5 or navigate away and back) | Skill details page reloads |
| 9 | Expand "Run settings" accordion | Run settings section displays |
| 10 | Verify Model field shows "Auto" | Auto selection persisted |

## Expected Final State

- Skill saved with run_settings.llm_settings.selection.mode = "auto"
- Auto selection persists after reload
- No fallback to fixed model occurs

## Pass/Fail Criteria

**Pass:**
- Auto model selection is saved correctly
- Auto persists after page reload
- Model selector displays "Auto" after reload

**Fail:**
- Auto selection is lost after reload
- Model reverts to project default or null
- Auto option is not available when it should be
