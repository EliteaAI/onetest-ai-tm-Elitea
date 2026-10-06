---
id: ELITEA-2270
title: "Build with AI can be cancelled without modifying the editor content"
priority: medium
type: functional
module: settings-project-params
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:settings]
requirements: []
---

# ELITEA-2270: Build with AI can be cancelled without modifying the editor content

**Module:** settings-project-params · **Priority:** medium · **Type:** functional

**Objective:** Verify that Build with AI can be cancelled without modifying the editor content. Success is confirmed when verify the project background editor content is unchanged.

---

## Preconditions

- User is logged in to the Elitea platform.


---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Settings → Project Context | Target page/section loads successfully. |
| 2 | Enter manual content in the Project Background editor | Field accepts the input and displays the entered value. |
| 3 | Click "Build with AI" to open the dialog | Control responds; expected next state is shown. |
| 4 | Close or cancel the dialog without submitting | Action completes without error and produces the expected UI state. |
| 5 | Verify the Project Background editor content is unchanged | Condition holds as described. |

---

## Expected Final State

Verify the Project Background editor content is unchanged.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Build with AI can be cancelled without modifying the editor content.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
