---
id: ELITEA-1873
title: "Generated skill draft fields are editable before creation"
priority: medium
type: functional
module: skills
status: draft
execution_type: automated
tags: [automated:UI:regression, feat:skills]
requirements: []
---

# ELITEA-1873: Generated skill draft fields are editable before creation

**Module:** skills · **Priority:** medium · **Type:** functional

**Objective:** Verify that the Name, Description, and Instructions fields in the Build with AI review form are editable, and that clicking "Create Skill" creates the skill with the user-edited values rather than the original generated values.

---

## Preconditions

- User is logged in to the Elitea platform with admin or editor role.
- A skill draft has been generated via the Build with AI modal.

---

## Test Data

| Field | Value |
|-------|-------|
| Modified Name | A valid modified skill name (lowercase, hyphens only) |
| Modified Description | A custom description text |
| Modified Instructions | Custom instruction text |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Generate a skill draft via Build with AI modal | The review/edit form is displayed with generated Name, Description, and Instructions |
| 2 | Modify the generated Name to a different valid value | The Name field accepts the edit and displays the new value |
| 3 | Modify the generated Description | The Description field accepts the edit and displays the new value |
| 4 | Modify the generated Instructions | The Instructions field accepts the edit and displays the new value |
| 5 | Verify all three fields accept the edits | All three fields reflect the user-entered values |
| 6 | Click "Create Skill" | Skill creation is initiated |
| 7 | Verify the Skill is created with the edited (not original generated) values | The created Skill shows the user-modified Name, Description, and Instructions |
| 8 | Verify the user is redirected to the created Skill details page | The Skill details page of the newly created Skill is displayed |

---

## Expected Final State

The Skill is successfully created with the user-edited values for Name, Description, and Instructions, and the user is on the Skill details page.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The Skill is created with edited values and the user lands on the Skill details page.

**Fail:**
- Any step produces an error or unexpected result.
- The Skill is created with the original generated values instead of the user-edited ones.
