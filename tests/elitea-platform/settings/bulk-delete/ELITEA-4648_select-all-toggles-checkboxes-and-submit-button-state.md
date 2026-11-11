---
id: ELITEA-4648
title: "Select all toggles all checkboxes and submit button state tracks selection"
priority: high
type: functional
module: settings-delete-project-data
status: draft
execution_type: manual
tags: [feat:settings, r-2.0.8]
requirements: [EliteaAI/elitea_issues#7189, EliteaAI/elitea_issues#7242]
---

## Preconditions

- Project with all seven entity types visible in Delete Project Data

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | With all checkboxes unchecked, observe "Delete selected data" | Button disabled |
| 2 | Click "Select all" | All seven checkboxes become checked; "Delete selected data" becomes enabled |
| 3 | Uncheck one individual checkbox | "Select all" reflects an indeterminate/unchecked state; "Delete selected data" remains enabled |
| 4 | Uncheck all remaining checkboxes one by one | "Delete selected data" becomes disabled once the last checkbox is unchecked |
| 5 | Click a single checkbox directly (not via Select all) | "Delete selected data" becomes enabled immediately |

## Expected Final State

Select all and the submit button state behave consistently with manual checkbox state at every step.

## Pass/Fail Criteria

**Pass:**
- Button state always accurately reflects whether ≥1 type is selected; Select all toggles all checkboxes correctly

**Fail:**
- Any inconsistency between checkbox state and button enablement, or Select all fails to toggle all checkboxes
