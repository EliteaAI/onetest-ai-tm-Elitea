---
id: ELITEA-4166
title: "Test connection always evaluates current unsaved form values and recognition indicator updates to match"
priority: critical
type: functional
module: model-settings
status: draft
execution_type: manual
tags: [feat:settings, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6793]
---

## Preconditions

- User is logged in to `{{base_url}}` as a project admin.
- An existing saved LLM model configuration exists that the tester can edit.

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/settings/ai-providers` |
| New valid Model Name | Different valid identifier than the saved one |
| New invalid Model Name | Misspelled/non-existent identifier |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open existing configuration for editing | Form loads with saved values. |
| 2 | Change Model Name to a different valid value, don't save | Recognition indicator updates to "Recognized". |
| 3 | Click Test connection | Result reflects the new unsaved value; success, consistent with indicator. |
| 4 | Change Model Name to an invalid value, don't save | Recognition indicator updates to "Not recognized". |
| 5 | Click Test connection again | Result reflects latest unsaved value; agrees with step 4. |

## Expected Final State

Test connection always reflects current unsaved form state; recognition indicator tracks each value consistently.

## Pass/Fail Criteria

**Pass:**
- Each result reflects the current field value and agrees with the recognition indicator.

**Fail:**
- A result reflects a stale value, or indicator disagrees with the result.
