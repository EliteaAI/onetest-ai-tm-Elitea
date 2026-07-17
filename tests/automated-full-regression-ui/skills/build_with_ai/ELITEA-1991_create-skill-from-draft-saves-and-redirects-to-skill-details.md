---
id: ELITEA-1991
title: "Create Skill from draft saves Skill and redirects to Skill details page"
priority: high
type: functional
module: skills
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:skills]
requirements: []
automation_test_id: tests.ui.skills.test_skill_build_with_ai.TestSkillBuildWithAIReviewFormEditableFields.test_create_skill_from_unmodified_draft_persists_generated_values
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/604
---

# ELITEA-1991: Create Skill from draft saves Skill and redirects to Skill details page

**Module:** skills · **Priority:** high · **Type:** functional

**Objective:** Verify that clicking "Create Skill" in the Build with AI review form saves the skill with the generated values, redirects the user to the Skill details page, and that the new skill appears in the Skills list.

---

## Preconditions

- User is logged in to the Elitea platform with admin or editor role.
- A skill draft has been generated via the Build with AI modal.
- The review/edit form is displayed.

---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Generate a skill draft via Build with AI modal | The review/edit form is displayed with generated values |
| 2 | Review the generated Name, Description, and Instructions without modifying them | All generated values are visible and correct |
| 3 | Click "Create Skill" | Skill creation is initiated |
| 4 | Verify the Skill is created in the current project | The Skill is saved to the current project |
| 5 | Verify the user is redirected to the Skill details page of the newly created Skill | The Skill details page of the new Skill is displayed |
| 6 | Verify the Skill details page shows the correct Name, Description, and Instructions from the draft | Name, Description, and Instructions match the generated draft values |
| 7 | Navigate to the Skills list and verify the new Skill appears there | The new Skill is listed on the Skills list page |

---

## Expected Final State

The Skill is created with generated values, the user is on the Skill details page showing correct data, and the Skill is visible in the Skills list.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The Skill is created, details match the draft, and it appears in the Skills list.

**Fail:**
- Any step produces an error or unexpected result.
- The Skill is not created, data does not match the draft, or the Skill does not appear in the Skills list.
