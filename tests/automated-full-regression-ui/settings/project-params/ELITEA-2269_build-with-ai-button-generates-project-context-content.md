---
id: ELITEA-2269
title: "Build with AI button generates project context content"
priority: medium
type: functional
module: settings-project-params
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:settings]
requirements: []
---

# ELITEA-2269: Build with AI button generates project context content

**Module:** settings-project-params · **Priority:** medium · **Type:** functional

**Objective:** Verify that Build with AI button generates project context content. Success is confirmed when verify the generated content is editable before saving.

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
| 2 | Click the "Build with AI" button | Control responds; expected next state is shown. |
| 3 | Verify a dialog or AI-assisted input appears | Condition holds as described. |
| 4 | Provide a description of the project when prompted | Action completes without error and produces the expected UI state. |
| 5 | Verify AI-generated content is inserted into the Project Background editor | Condition holds as described. |
| 6 | Verify the generated content is editable before saving | Condition holds as described. |

---

## Expected Final State

Verify the generated content is editable before saving.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Build with AI button generates project context content.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
