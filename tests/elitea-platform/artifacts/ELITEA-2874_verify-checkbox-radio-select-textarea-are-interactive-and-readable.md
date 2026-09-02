---
id: ELITEA-2874
title: "Verify checkbox, radio, select, and textarea controls are interactive and readable by JS"
priority: medium
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [feat:artifacts, comm:feedback, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6176]
---

## Preconditions

- User is logged in to `{{base_url}}`
- An artifact bucket exists and is available for file upload

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| File | `form-controls-test.html` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Upload `form-controls-test.html` and open in Preview mode | All controls render |
| 2 | Toggle the checkbox | Result line shows **PASS** with correct checked/unchecked state |
| 3 | Select a radio option | Result line shows **PASS** with correct selected value |
| 4 | Change the select dropdown | Result line shows **PASS** with correct selected value |
| 5 | Type into the textarea | Result line shows **PASS** with current textarea value |
| 6 | Check for error banners | No error banner is shown for any of the four controls |

## Expected Final State

All common form control types are fully interactive and their state is correctly readable by inline JS event listeners.

## Pass/Fail Criteria

**Pass:**
- All four controls (checkbox, radio, select, textarea) report PASS with correct values

**Fail:**
- Any control fails to respond to interaction or reports an incorrect value
