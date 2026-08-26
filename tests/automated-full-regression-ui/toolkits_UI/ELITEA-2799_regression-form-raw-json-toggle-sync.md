---
id: ELITEA-2799
title: "Regression - Form and Raw JSON Toggle Synchronization"
priority: high
type: regression
module: toolkits-indexes
status: draft
execution_type: manual
tags: [regression, toolkit-redesign, configuration]
requirements: []
---
# ELITEA-2799: Regression - Form and Raw JSON Toggle Synchronization

**Module:** Toolkits & Indexes · **Priority:** High · **Type:** Regression

**Objective:** Verify Form and Raw JSON views remain synchronized when toggling between them.

**Coverage:**
- Form view displays correctly
- Raw JSON view displays valid JSON
- Changes in Form reflect in JSON
- Changes in JSON reflect in Form
- No data loss on toggle

## Preconditions

- Logged in to {{base_url}} with edit permissions
- An existing toolkit

## Test Data

| Field | Value |
|-------|-------|
| Toolkit | Any configurable toolkit |
| Test Description | "Regression Test Description" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Toolkit Details page. | Form view displays by default. |
| 2 | Note current Description value. | Value recorded. |
| 3 | Change Description to "Regression Test Description". | Field updated. |
| 4 | Click "Raw JSON" toggle. | View switches to JSON editor. |
| 5 | Verify JSON contains the new Description value. | JSON shows updated description. |
| 6 | In JSON, modify another field value. | JSON edited. |
| 7 | Click "Form" toggle. | View switches to Form. |
| 8 | Verify the JSON change is reflected in Form. | Form field shows updated value. |
| 9 | Toggle back and forth 3 more times. | No data loss; values consistent. |

## Expected Final State

Both views remain synchronized with no data loss across multiple toggles.

## Pass/Fail Criteria

**Pass:**
- Toggle switches views correctly
- Form changes appear in JSON
- JSON changes appear in Form
- No data loss on repeated toggling

**Fail:**
- Toggle doesn't work
- Views out of sync
- Data lost on toggle
- Invalid JSON displayed
