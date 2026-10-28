---
id: ELITEA-4194
title: "Verify publishing skill with private model is rejected with 'select shared model' error"
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
- User has permission to publish skills to catalog
- A skill with run_settings configured with a PRIVATE model exists (model from user's project, not shared)

## Test Data

| Field | Value |
|-------|-------|
| Skill | Skill with private model in run_settings |
| Model | Private model (not shared/public) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to skill with private model configured | Skill details page opens |
| 2 | Verify "Run settings" → Model is a private/project-specific model | Model: Private project model |
| 3 | Click "Publish" button | Publish dialog or validation starts |
| 4 | Attempt to publish skill | Publish operation blocked |
| 5 | Observe error message | Error displayed: "Select a shared model or clear the model to publish this skill" or similar |
| 6 | Verify skill is NOT published | Skill status remains unpublished |
| 7 | Verify catalog does NOT show the skill | Skill not in catalog |
| 8 | Navigate back to skill editor → Change model to a shared/public model → Attempt publish again | Publish validation passes |
| 9 | OR clear model (set to null/default) → Attempt publish again | Publish validation passes |

## Expected Final State

- Publishing blocked when skill has private model
- Clear error message guides user to select shared model or clear model
- Skill not published with private model
- User can fix by selecting shared model or clearing model

## Pass/Fail Criteria

**Pass:**
- Publish operation blocked with private model
- Error message clearly states: "Select a shared model or clear the model"
- Skill not published
- Publishing succeeds after selecting shared model or clearing model

**Fail:**
- Skill published with private model
- No error message shown
- Unclear error message
- User cannot publish even after selecting shared model
