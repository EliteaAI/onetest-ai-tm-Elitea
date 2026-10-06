---
id: ELITEA-1988
title: "Clicking Build with AI opens the generation modal"
priority: high
type: functional
module: skills
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:skills]
requirements: []
---

# ELITEA-1988: Clicking Build with AI opens the generation modal

**Module:** skills · **Priority:** high · **Type:** functional

**Objective:** Verify that clicking the "Build with AI" / Magic Wand button opens the generation modal and that the modal contains the expected UI elements: a natural-language prompt input field, a "Generate" button, and a "Cancel" button.

---

## Preconditions

- User is logged in to the Elitea platform with admin or editor role.
- The New Skill creation screen is accessible.

---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Log in as admin or editor | Login is successful and the user is on the platform home |
| 2 | Navigate to the New Skill creation screen | The New Skill creation screen is displayed |
| 3 | Click the "Build with AI" / Magic Wand button | The Build with AI modal opens |
| 4 | Verify the modal contains a natural-language prompt input field | A text input field for natural-language prompts is visible in the modal |
| 5 | Verify the modal contains a "Generate" button | The "Generate" button is visible in the modal |
| 6 | Verify the modal contains a "Cancel" button | The "Cancel" button is visible in the modal |

---

## Expected Final State

The Build with AI modal is open and displays all required elements: a natural-language prompt input, a "Generate" button, and a "Cancel" button.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The modal opens correctly and all three UI elements (prompt input, Generate button, Cancel button) are present.

**Fail:**
- Any step produces an error or unexpected result.
- The modal does not open, or one or more required elements are missing.
