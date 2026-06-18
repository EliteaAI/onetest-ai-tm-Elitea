---
id: ELITEA-0806
title: "Collapsed STATE panel: icon reflects whether a default value is set"
priority: medium
type: functional
module: pipelines
status: ready
execution_type: manual
tags: [issue:2676, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#2676]
---
# ELITEA-0806: Collapsed STATE panel: icon reflects whether a default value is set

**Module:** Pipelines · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that in the collapsed STATE panel, variables with a default value show the sliders icon (≡) and variables without show the + icon, while built-in `input`/`messages` toggles are unaffected.

**Coverage:**
- Variables with a default value → ≡ icon next to type badge
- Variables without a default value → + icon next to type badge
- `input` and `messages` built-ins show toggle only — unaffected

## Preconditions

- Logged in to {{base_url}} with a valid user account
- A Pipeline exists with at least 2 custom state variables with default values (e.g. json, number, string) and 2 custom state variables with no default value (e.g. str_null, list_null)

## Test Data

- Variable with default: e.g. number = 911, string = ["a","b"]
- Variable without default: e.g. str_null, list_null (empty)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the Pipelines page. Open a pipeline that has custom state variables, some with default values and some without. | Pipeline detail page opens. |
| 2 | Click the STATE panel icon (or open the States sidebar) to view the variable list in collapsed state. | STATE panel opens showing all variables in their collapsed/single-row state. |
| 3 | Observe the icon next to the type badge for a variable that has a default value configured. | The sliders/settings icon (≡) is displayed next to the type badge. |
| 4 | Observe the icon next to the type badge for a variable that has no default value. | The + icon is displayed next to the type badge. |
| 5 | Observe the `input` and `messages` built-in variables. | Both show their toggle switch only — no ≡ or + icon. They are unaffected by the change. |

## Expected Final State

Both show their toggle switch only — no ≡ or + icon. They are unaffected by the change.

## Pass/Fail Criteria

**Pass:**
- ≡ shown for variables with defaults; + shown for variables without
- Built-in variable toggles unaffected

**Fail:**
- Icons missing, incorrect, or built-in variable toggles broken
