---
id: ELITEA-0808
title: "Expand icon (↗) opens larger editor popup from inline input field"
priority: medium
type: functional
module: pipelines
status: ready
execution_type: manual
tags: [issue:2676, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#2676]
---
# ELITEA-0808: Expand icon (↗) opens larger editor popup from inline input field

**Module:** Pipelines · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that when a variable is in the expanded/inline-edit state, the expand icon (↗) is visible and opens a full larger editor popup, and that changes made in the popup are reflected back in the inline field.

**Coverage:**
- Expand icon (↗) visible when variable is in inline-edit state
- Clicking ↗ opens a larger editor popup
- Changes in popup reflected in inline field on close

## Preconditions

- Logged in to {{base_url}} with a valid user account
- A Pipeline with at least one custom state variable (with or without a default value)

## Test Data

- Variable: e.g. json (type: JSON), value: {"name": "sam"}
- Updated value in popup: {"name": "sam", "role": "admin"}

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the Pipeline. Open the STATE panel. Click the + or ≡ icon on a variable to expand it into inline-edit state. | Variable row shows the inline input field. |
| 2 | Locate the expand icon (↗) on the right side of the inline input field. | Expand icon (↗) is visible. |
| 3 | Click the expand icon (↗). | A larger editor popup opens for the variable value. |
| 4 | Edit the value in the popup (e.g. add a field to the JSON). Close or confirm the popup. | Popup closes. The updated value is reflected in the inline input field. |
| 5 | Save the pipeline and reopen it. Verify the value is retained. | Updated value persists after save and reload. |

## Expected Final State

Updated value persists after save and reload.

## Pass/Fail Criteria

**Pass:**
- ↗ icon visible in expanded state; click opens popup; popup changes reflected in inline field; value persists after save

**Fail:**
- ↗ icon not visible; popup does not open; changes not reflected in inline field
