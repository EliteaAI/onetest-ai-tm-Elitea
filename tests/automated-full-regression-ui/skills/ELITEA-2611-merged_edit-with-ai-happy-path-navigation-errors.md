---
id: ELITEA-2611
title: "Skill — Edit with AI (Happy Path, Navigation, Errors)"
priority: high
type: functional
module: skills
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:skills, feat:edit-with-ai, regression:merged]
requirements: []
---

# ELITEA-2611: Skill — Edit with AI (Happy Path, Navigation, Errors)

**Module:** skills · **Priority:** high · **Type:** functional

**Objective:** Verify complete Edit with AI feature for skills including happy path (prompt, generation, checkbox selection, apply), navigation (back preserves prompt, cancel preserves original), and error handling (empty prompt validation, generation failure with retry). Success is confirmed when all Edit with AI workflows work correctly.

---

## Preconditions

- User is logged in to the Elitea platform.
- A project exists and is accessible.
- User has Admin or Editor permissions (Edit with AI feature is not visible to Viewers).

---

## Test Data

| Field | Value |
|-------|-------|
| Skill Name | Edit with AI Test Skill |
| Original Skill Description | Original description for testing Edit with AI |
| Original Skill Instructions | Original instructions content that needs improvement. This is the baseline text. |
| Edit with AI Prompt | Improve the instructions to be more detailed and add examples |
| Empty Prompt | (empty string) |
| Failure Simulation Prompt | (if available: prompt that causes generation to fail, or simulate backend failure) |

---

## Steps

### Part 1: Happy Path — Edit with AI Workflow

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create a new skill with Name "Edit with AI Test Skill", Description "Original description for testing Edit with AI", Instructions "Original instructions content that needs improvement. This is the baseline text." | Skill is created successfully |
| 2 | Open the skill "Edit with AI Test Skill" | Skill editor page loads with original content |
| 3 | Click "Edit with AI" button or CTA | Edit with AI wizard/modal opens |
| 4 | Verify the Edit with AI interface displays: prompt input field, generate button | Interface displays correctly |
| 5 | Enter prompt: "Improve the instructions to be more detailed and add examples" | Prompt is entered in the input field |
| 6 | Click "Generate" or "Submit" button | Generation process starts (loading indicator may appear) |
| 7 | Wait for generation to complete | Wizard advances to comparison step |
| 8 | Verify the wizard displays: current content vs. suggested content in side-by-side or comparison view | Comparison view is displayed |
| 9 | Verify each suggested change has a checkbox for selection | Checkboxes are present for each suggestion |
| 10 | Verify "Apply" or "Apply Selected" button is visible | Apply button is visible |
| 11 | Uncheck one or more suggested changes (leave at least one checked) | Checkboxes are unchecked |
| 12 | Click "Apply Selected" or "Apply" button | Wizard closes; editor updates with selected suggestions |
| 13 | Verify ONLY the checked suggestions are applied to the skill | Only selected suggestions are applied; unchecked suggestions are not applied |
| 14 | Verify unchecked suggestions remain unchanged in the original content | Original content is preserved where suggestions were unchecked |
| 15 | Click Save | Skill is saved with applied AI edits |
| 16 | Re-open the skill and verify the applied changes persist | Changes are saved and persist after reload |

### Part 2: Navigation — Back Button Preserves Prompt

| # | Action | Expected Result |
|---|--------|-----------------|
| 17 | Open the skill "Edit with AI Test Skill" | Skill editor page loads |
| 18 | Click "Edit with AI" button | Edit with AI wizard opens |
| 19 | Enter prompt: "Make the instructions shorter and more concise" | Prompt is entered |
| 20 | Click "Generate" | Generation starts |
| 21 | Wait for comparison view to load | Comparison view is displayed |
| 22 | Click "Back" button (if available in the wizard) | Wizard returns to the prompt input step |
| 23 | Verify the prompt "Make the instructions shorter and more concise" is still present in the input field | Prompt is preserved after navigation back |
| 24 | Click "Generate" again | Generation runs again with the preserved prompt |
| 25 | Verify comparison view loads successfully | Wizard works correctly after back navigation |

### Part 3: Navigation — Cancel Preserves Original Content

| # | Action | Expected Result |
|---|--------|-----------------|
| 26 | With the comparison view open, click "Cancel" or "Close" button | Wizard closes |
| 27 | Verify the skill editor content remains unchanged (original content is preserved) | Original content is still displayed; no AI suggestions were applied |
| 28 | Verify no changes were saved | Skill content is identical to before opening Edit with AI |

### Part 4: Error Handling — Empty Prompt Validation

| # | Action | Expected Result |
|---|--------|-----------------|
| 29 | Open the skill "Edit with AI Test Skill" | Skill editor page loads |
| 30 | Click "Edit with AI" button | Edit with AI wizard opens |
| 31 | Leave the prompt field empty | Prompt field is blank |
| 32 | Click "Generate" button | Generation is blocked or validation error appears |
| 33 | Verify validation message appears: "Prompt cannot be empty" or similar | Clear validation error message is displayed |
| 34 | Verify "Generate" button is disabled or generation does not proceed | Generation is blocked |

### Part 5: Error Handling — Generation Failure with Retry

| # | Action | Expected Result |
|---|--------|-----------------|
| 35 | Enter a valid prompt in the Edit with AI wizard | Prompt is entered |
| 36 | (If possible) simulate a generation failure by: entering a problematic prompt, disconnecting network temporarily, or using test mode to trigger failure | Setup for failure simulation |
| 37 | Click "Generate" | Generation starts and fails |
| 38 | Verify error message is displayed: "Generation failed. Please try again." or similar | Clear error message is displayed |
| 39 | Verify "Retry" or "Try Again" button is visible | Retry button is available |
| 40 | Click "Retry" or "Try Again" | Generation is attempted again |
| 41 | If generation succeeds on retry, verify comparison view is displayed | Retry mechanism works correctly |
| 42 | If generation fails again, verify error message persists and retry option remains available | Error handling is robust |

---

## Expected Final State

- Edit with AI wizard completes successfully with prompt input, generation, comparison, and selective apply
- Back button preserves the prompt for re-generation
- Cancel button preserves original content without applying AI suggestions
- Empty prompt is validated and blocks generation with clear error message
- Generation failures display clear error message with retry option
- Only selected (checked) suggestions are applied to the skill
- All applied changes persist after save and reload

---

## Pass/Fail Criteria

**Pass:**
- Edit with AI happy path completes: prompt → generate → comparison → selective apply (checkboxes work)
- Only checked suggestions are applied; unchecked suggestions are not applied
- Back button preserves prompt for re-generation
- Cancel button preserves original content (no changes applied)
- Empty prompt validation blocks generation with clear error message
- Generation failure displays error message with retry option
- All applied changes persist correctly

**Fail:**
- Edit with AI wizard does not open or fails to complete
- All suggestions are applied regardless of checkbox selection
- Back button does not preserve prompt or causes error
- Cancel applies changes instead of preserving original
- Empty prompt is not validated or validation message is unclear
- Generation failure has no error message or no retry option
- Applied changes do not persist after save
- Any step produces an error or unexpected result

---

## Notes

**Source functional tests:** ELITEA-2611, ELITEA-2612

**Regression rationale:** Consolidated from 2 tests covering Edit with AI feature: (1) ELITEA-2611 tests happy path (multi-step wizard, current vs. suggested comparison, checkbox selection, apply only checked suggestions), and (2) ELITEA-2612 tests navigation (back button preserves prompt, cancel preserves original) and error handling (empty prompt validation, generation failure with retry). These tests cover different aspects of the same feature and can be merged into a comprehensive Edit with AI test.

**Selected checkpoints:**
- Happy path: prompt → generate → comparison → checkbox selection → apply selected → persist
- Back button → prompt preserved → generate again
- Cancel → original content preserved
- Empty prompt → validation error → generation blocked
- Generation failure → error message → retry available
