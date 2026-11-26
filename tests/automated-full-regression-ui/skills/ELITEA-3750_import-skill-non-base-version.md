---
id: ELITEA-3750
title: "Import Skill Non-Base Version"
priority: medium
type: functional
module: skills
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:skills]
requirements: []
automation_test_id: tests.ui.skills.test_skill_export_import.TestSkillExportImportNonBaseVersion.test_import_skill_non_base_version
---

# ELITEA-3750: Import Skill Non-Base Version

**Module:** skills · **Priority:** medium · **Type:** functional

**Objective:** Verify that exporting a non-base version of a skill and importing it creates a new skill with a `base` version, with all fields populated correctly and the skill editable without errors.

---

## Preconditions

- User is logged in to the Elitea platform.
- A project exists and is accessible.
- The Skills section is available in the project with export and import capabilities.

---

## Test Data

| Field | Value |
|-------|-------|
| Initial skill version | base |
| Additional version name | ver_1 |
| Version to export | ver_1 |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create a Skill with a `base` version, switch the Instructions section to Edit mode (click the "Edit mode" toggle; detail page opens in Preview), modify the instructions, and save as a new version named `ver_1` | Skill has both `base` and `ver_1` versions saved successfully |
| 2 | Switch to the `ver_1` version and export this version of the Skill | A `.md` file is downloaded representing the `ver_1` version |
| 3 | Import the exported `.md` file via the Skills import feature | Import completes without errors; a new Skill entry appears in the Skills list |
| 4 | Open the imported Skill and verify it has a `base` version created | The imported Skill shows a `base` version (not `ver_1`) |
| 5 | Verify all fields (name, description, instructions, tags) are populated correctly | All fields match the content from the exported `ver_1` version |
| 6 | Edit a field on the imported Skill and save | Skill saves without errors; changes are persisted |

---

## Expected Final State

The imported Skill exists as a new entry with a `base` version (regardless of the exported version name), all fields are correctly populated from the export, and the skill can be edited and saved without errors.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Imported Skill has a `base` version with all fields correctly populated and is editable.

**Fail:**
- Any step produces an error or unexpected result.
- Imported Skill does not have a `base` version, fields are missing or incorrect, or the Skill cannot be saved after editing.
