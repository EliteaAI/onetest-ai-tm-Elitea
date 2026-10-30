---
id: ELITEA-1988
title: "Build with AI — Complete Happy Path (Generate, Edit, and Create Skill)"
priority: critical
type: functional
module: skills
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:skills]
requirements: []
---

# ELITEA-1988: Build with AI — Complete Happy Path (Generate, Edit, and Create Skill)

**Module:** skills · **Priority:** critical · **Type:** functional

**Objective:** Verify the complete end-to-end happy path flow for Build with AI: opening the modal, generating a skill draft from a natural-language prompt, editing the generated fields, creating the skill, and verifying the skill appears in the list and details page.

---

## Preconditions

- User is logged in to the Elitea platform with admin or editor role.
- The New Skill creation screen is accessible.
- The Skills page is accessible.

---

## Test Data

| Field | Value |
|-------|-------|
| Natural-language description | "A skill that helps write concise GitHub PR review comments" |
| Modified Name | "pr-review-helper" |
| Modified Description | "Generates concise and actionable code review comments for GitHub pull requests" |
| Modified Instructions | "Analyze the provided code diff and generate 3-5 specific, actionable review comments focusing on code quality, potential bugs, and best practices." |

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
| 7 | Enter the natural-language description: "A skill that helps write concise GitHub PR review comments" | The input field accepts and displays the entered description |
| 8 | Click "Generate" | Generation is initiated |
| 9 | Verify the modal shows a loading state with text "Generating skill draft..." | The modal displays the loading state and "Generating skill draft..." text |
| 10 | Wait for generation to complete | Generation completes and the modal transitions |
| 11 | Verify the modal transitions to a review/edit form showing generated: Name, Description, Instructions | The review/edit form is shown with generated Name, Description, and Instructions fields populated |
| 12 | Verify no suggested tools, agents, pipelines, toolkits, MCPs, or resources section is shown | No suggested tools, agents, pipelines, toolkits, MCPs, or resources are displayed |
| 13 | Verify the generated Name field is populated and follows naming rules | The Name field contains a valid generated name (lowercase, hyphens, no leading/trailing hyphens) |
| 14 | Verify the generated Description field is populated | The Description field contains generated text |
| 15 | Verify the generated Instructions field is populated | The Instructions field contains generated text |
| 16 | Modify the Name field to "pr-review-helper" | The Name field accepts the edit and displays "pr-review-helper" |
| 17 | Modify the Description field to the test data value | The Description field accepts the edit and displays the new value |
| 18 | Modify the Instructions field to the test data value | The Instructions field accepts the edit and displays the new value |
| 19 | Click "Create Skill" | Skill creation is initiated |
| 20 | Verify the user is redirected to the Skill details page of the newly created Skill | The Skill details page of the new Skill is displayed |
| 21 | Verify the Skill details page shows the edited Name: "pr-review-helper" | Name on details page matches the edited value |
| 22 | Verify the Skill details page shows the edited Description | Description on details page matches the edited value |
| 23 | Verify the Skill details page shows the edited Instructions | Instructions on details page matches the edited value |
| 24 | Navigate to the Skills list page | The Skills list page is displayed |
| 25 | Verify the new Skill "pr-review-helper" appears in the Skills list | The new Skill is listed on the Skills list page |

---

## Expected Final State

- The Skill "pr-review-helper" is successfully created with user-edited values.
- The user is on the Skill details page showing the correct edited Name, Description, and Instructions.
- The Skill appears in the Skills list.

---

## Pass/Fail Criteria

**Pass:**
- All assertions verified:
  - Modal opens with all required UI elements (prompt input, Generate button, Cancel button)
  - Generation completes successfully with loading state shown
  - Review form displays with generated Name, Description, Instructions (no extra sections)
  - All three fields are editable
  - Skill is created with edited values (not original generated values)
  - Skill details page displays correct edited values
  - Skill appears in Skills list

**Fail:**
- Any assertion fails:
  - Modal does not open or is missing required elements
  - Generation fails or does not show loading state
  - Review form is missing fields or shows forbidden sections
  - Fields are not editable
  - Skill is created with original generated values instead of edits
  - Skill details do not match edited values
  - Skill does not appear in Skills list

---

## Notes

**Source functional tests:** ELITEA-1988, ELITEA-1989, ELITEA-1990, ELITEA-1991

**Regression rationale:** Consolidated from 4 tests to cover the complete happy path in one flow: modal opening → generation → field population → editing → creation → verification. This eliminates redundant setup and modal opening steps while preserving all critical assertions.

**Selected checkpoints:** Modal UI elements, generation loading state, generated field presence and validity, field editability, skill creation with edited values, redirect to details page, Skills list appearance.
