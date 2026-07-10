---
id: ELITEA-1737
title: "Import Skill (Base Version)"
priority: medium
type: functional
module: skills
status: ready
execution_type: automated
automation_test_id: tests.ui.skills.test_skill_export_import.TestSkillExportImport.test_export_and_import_skill_base_version
tags: [automated:UI:regression, feat:skills]
requirements: []
---

# ELITEA-1737: Import Skill (Base Version)

**Module:** skills · **Priority:** medium · **Type:** functional

**Objective:** Verify that a skill's `base` version can be exported as a `.md` file containing all required fields, and that importing the file creates a new skill with a unique ID and a fully populated `base` version.

---

## Preconditions

- User is logged in to the Elitea platform.
- A project exists and is accessible.
- The Skills section is available in the project.
- The Skills → Import feature is available.

---

## Test Data

| Field | Value |
|-------|-------|
| Skill name | (any descriptive name, e.g. "Test Export Skill") |
| Skill version to export | base |
| Expected export file format | `.md` |
| Expected fields in exported file | name, description, version, tags, instructions |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create a Skill with instructions, description, name, and tags | Skill is created and saved successfully with all fields populated |
| 2 | Export the `base` version of the Skill | A file is downloaded; the file has a `.md` extension |
| 3 | Open the exported `.md` file and verify its contents | File contains: name, description, version, tags, and instructions fields |
| 4 | Navigate to Skills → Import and import the exported `.md` file | Import completes without errors; a new Skill entry appears in the Skills list |
| 5 | Verify the imported Skill has a new unique ID | The imported Skill's ID is different from the source Skill's ID |
| 6 | Verify the `base` version exists on the imported Skill and instructions are populated | `base` version is present and instructions match the exported content |
| 7 | Save the imported Skill | Skill saves without errors; no validation or save errors are shown |

---

## Expected Final State

A new Skill exists in the system with a unique ID, a `base` version, and all fields (name, description, tags, instructions) correctly populated from the imported `.md` file.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Imported Skill has a unique ID, `base` version is present, and all fields are correctly populated.

**Fail:**
- Any step produces an error or unexpected result.
- The exported file is not `.md`, missing required fields, the imported Skill ID duplicates the source, or the Skill cannot be saved after import.
