---
id: ELITEA-1997
title: "Build with AI — Cancel Behavior (All Steps)"
priority: high
type: functional
module: skills
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:skills]
requirements: []
---

# ELITEA-1997: Build with AI — Cancel Behavior (All Steps)

**Module:** skills · **Priority:** high · **Type:** functional

**Objective:** Verify that clicking "Cancel" at any step of the Build with AI flow (prompt input step or review step) closes the modal without creating a Skill, leaves the New Skill form empty, and does not add any skill to the Skills list.

---

## Preconditions

- User is logged in to the Elitea platform with admin or editor role.
- The New Skill creation screen is accessible.
- The Skills page is accessible.

---

## Test Data

| Field | Value |
|-------|-------|
| Natural-language description | "A skill that helps generate unit tests" |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| **Cancel from Prompt Input Step** | | |
| 1 | Navigate to the New Skill creation screen | The New Skill creation screen is displayed |
| 2 | Click the "Build with AI" / Magic Wand button | The Build with AI modal opens with the prompt input field |
| 3 | Enter a natural-language description: "A skill that helps generate unit tests" | The input field accepts and displays the description |
| 4 | Click "Cancel" | The modal closes |
| 5 | Verify the modal is no longer visible | The modal has closed |
| 6 | Verify the New Skill form is still shown with empty fields (no auto-population from the cancelled draft) | The New Skill creation form is displayed with empty fields |
| 7 | Navigate to the Skills list | The Skills list page is displayed |
| 8 | Verify no new Skill was created | No new Skill entry appears in the Skills list |
| **Cancel from Review Step** | | |
| 9 | Return to the New Skill creation screen | The New Skill creation screen is displayed |
| 10 | Click the "Build with AI" / Magic Wand button | The Build with AI modal opens |
| 11 | Enter a natural-language description: "A skill that helps generate unit tests" | The input field accepts and displays the description |
| 12 | Click "Generate" | Generation is initiated |
| 13 | Wait for generation to complete | Generation completes and the review/edit form is displayed with generated values |
| 14 | Verify the review/edit form is displayed with generated Name, Description, and Instructions | The review/edit form shows generated values |
| 15 | Click "Cancel" | The modal closes |
| 16 | Verify the modal is no longer visible | The modal has closed |
| 17 | Navigate to the Skills list | The Skills list page is displayed |
| 18 | Verify no new Skill was created (no entry corresponding to the cancelled draft) | No new Skill entry corresponding to the cancelled draft appears in the Skills list |

---

## Expected Final State

- Clicking "Cancel" from the prompt input step closes the modal, leaves the New Skill form empty, and creates no Skill.
- Clicking "Cancel" from the review step closes the modal and creates no Skill.
- The Skills list remains unchanged after both cancel operations.

---

## Pass/Fail Criteria

**Pass:**
- All assertions verified:
  - Modal closes when "Cancel" is clicked from prompt input step
  - New Skill form remains empty after cancelling from prompt input step
  - No Skill is created after cancelling from prompt input step
  - Modal closes when "Cancel" is clicked from review step
  - No Skill is created after cancelling from review step
  - Skills list is unchanged after both cancel operations

**Fail:**
- Any assertion fails:
  - Modal does not close
  - New Skill form is auto-populated after cancel from prompt input step
  - A Skill is created after clicking "Cancel" from either step
  - Skills list shows a new entry after cancel

---

## Notes

**Source functional tests:** ELITEA-1997, ELITEA-1998

**Regression rationale:** Consolidated from 2 tests to verify cancel behavior at both steps (prompt input and review) in a single flow. This eliminates redundant setup and navigation steps while preserving all critical assertions about modal closure and no-skill-creation.

**Selected checkpoints:** Modal closure after cancel, New Skill form state (empty) after cancel from prompt step, no Skill creation after cancel from either step, Skills list unchanged.
