---
id: ELITEA-1102
title: "S3 API Credential Creation Form — User ID Field Is Empty by Default"
priority: medium
type: functional
module: toolkits-credentials
status: ready
execution_type: manual
tags: [feat:credentials, eng:design, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3838]
---
# ELITEA-1102: S3 API Credential Creation Form — User ID Field Is Empty by Default

**Module:** Toolkits Credentials · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that the User ID field in the S3 API credential creation form is empty by default and does not contain a pre-populated value (e.g. "0") when the form is first opened.

**Coverage:**
- User ID field renders empty on initial form load
- No default numeric value "0" is pre-filled in the User ID field
- Placeholder text (if any) does not constitute a pre-filled value
- Field behavior applies in both Private and Team project contexts

## Preconditions

- Logged in to ELITEA (`{{base_url}}`)

## Test Data

- Credential type: S3 API
- Expected User ID field state on open: empty (e.g. no value, not "0" not "-1")

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the Credentials section from the left sidebar. | The Credentials page loads and displays the existing credentials list (or empty state). |
| 2 | Click the + Create button. | A dialog appears prompting to select a credential type. |
| 3 | Select S3 API as the credential type. | The S3 API credential creation form renders with all its fields. |
| 4 | Immediately observe the User ID field — do NOT click or interact with it yet. | The User ID field is empty (no value displayed, no "0" pre-filled). |
| 5 | Inspect the User ID field for placeholder text. | If placeholder text is present, it is descriptive (e.g. "Enter User ID") and does NOT display "0" as a placeholder. |
| 6 | Close the form without saving and reopen it by clicking + Create → S3 API again. | On the second open, the User ID field is still empty — no value persists from previous open. |
| 7 | Repeat steps 1–4 in a Team project context (switch to a Team project and navigate to Credentials → + Create → S3 API). | The User ID field is also empty in the Team project context. |

## Expected Final State

The User ID field is also empty in the Team project context.

## Pass/Fail Criteria

**Pass:**
- User ID field is empty upon initial form render in both Private and Team project contexts
- No "0" value appears in the User ID field at any point during steps 1–7
- Placeholder text (if present) is descriptive and does not show "0"
- Re-opening the form does not introduce any pre-filled value

**Fail:**
- The User ID field displays "0" or any other value at any point during form open (before user interaction)
- Placeholder text shows "0"
