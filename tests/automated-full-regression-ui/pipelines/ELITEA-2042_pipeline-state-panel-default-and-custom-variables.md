---
id: ELITEA-2042
title: "Pipeline — State Panel (Default and Custom Variables)"
priority: high
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:pipelines]
requirements: []
---

# ELITEA-2042: Pipeline — State Panel (Default and Custom Variables)

**Module:** pipelines · **Priority:** high · **Type:** functional

**Objective:** Verify that the State panel displays immutable default variables (input, messages), allows adding custom variables with type selection, and that custom variables appear in node Input/Output comboboxes and in the YAML state section.

---

## Preconditions

- User is logged in to the Elitea platform.
- A pipeline is open in Flow view.

---

## Test Data

| Field | Value |
|-------|-------|
| Custom variable name | custom_output |
| Custom variable type | String |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open a pipeline in Flow view | Pipeline canvas is displayed |
| 2 | Click the "State" button above the canvas | STATE panel opens on the right side |
| 3 | Verify STATE panel opens with close (X) button | Panel is visible with a close button |
| 4 | Verify default immutable state variables present: "input" (str, toggle on) and "messages" (list, toggle on) — these cannot be deleted or renamed | Both "input" and "messages" are listed without delete buttons |
| 5 | Click "+" button to add a new state variable | New variable input appears |
| 6 | Enter variable name: "custom_output" | Name field is populated |
| 7 | Click type button (shows "Abc" for String by default) — verify dropdown with types: String (Abc), Number (#), List, Json | Type dropdown shows all 4 options |
| 8 | Select desired type (e.g., keep as String) | String type is selected |
| 9 | Verify new variable "custom_output" appears in the State panel list | "custom_output" is listed in the panel |
| 10 | Save pipeline | Pipeline saves without errors |
| 11 | Switch to Yaml view — verify "state:" section contains: input (type: str), messages (type: list), custom_output (type: str, value: '') | YAML state section includes all variables |
| 12 | Verify "custom_output" is now available in node Input/Output combobox dropdowns | "custom_output" appears as an option in node comboboxes |

---

## Expected Final State

The State panel shows default immutable variables (input, messages) and the newly added "custom_output" variable. The YAML state section reflects all variables and "custom_output" is available in node comboboxes.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- State panel works correctly, YAML state section is accurate, and custom variable is available in comboboxes.

**Fail:**
- Any step produces an error or unexpected result.
- Custom variable is not saved, not in YAML, or not available in comboboxes.
