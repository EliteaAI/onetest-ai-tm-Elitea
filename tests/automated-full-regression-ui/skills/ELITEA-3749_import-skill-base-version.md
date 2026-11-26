---
id: ELITEA-3749
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

# ELITEA-3749: Import Skill (Base Version)

**Module:** skills · **Priority:** medium · **Type:** functional

**Objective:** Verify that a skill's `base` version can be exported as a `.md` file containing all required fields, and that importing the file creates a new skill with a unique ID and a fully populated `base` version.

---

## Preconditions

- User is logged in to the Elitea platform.
- A project exists and is accessible.
- The Skills section is available in the project.
- The Skills → **Add** → **Import from file** feature is available.
- The Skill created in step 1 has no files (**Files – 0**), so it exports as `.md`.

---

## Test Data

| Field | Value |
|-------|-------|
| Skill name | (any descriptive name, e.g. "Test Export Skill") |
| Skill version to export | base |
| Expected export file format | `.md` |
| Skill licence | `license: MIT` (added in the frontmatter editor) |
| Skill run settings | A non-default model, Custom max tokens, a reasoning effort |
| Expected fields in exported file | Top level: name, description, license, metadata. `metadata`: elitea-tags, elitea-model, elitea-max-tokens, elitea-reasoning-effort. Instructions body |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create a Skill with instructions, description, name, tags, a licence (`license: MIT` in the frontmatter) and the run settings from Test Data | Skill is created and saved successfully with all fields populated |
| 2 | Export the `base` version of the Skill | A file is downloaded; the file has a `.md` extension |
| 3 | Open the exported `.md` file and verify its contents | Top level has only spec keys (`name`, `description`, `license`, `metadata`). `metadata` contains `elitea-tags` (a JSON array string), `elitea-model`, `elitea-max-tokens` and `elitea-reasoning-effort`. The instructions body is present |
| 4 | Open Skills → **Add** → **Import from file**, choose the exported `.md` file, then click **Import** in the **Import parameters** dialog | Import completes without errors; a new Skill entry appears in the Skills list |
| 5 | Verify the imported Skill has a new unique ID | The imported Skill's ID is different from the source Skill's ID |
| 6 | Verify the `base` version exists on the imported Skill and instructions are populated | `base` version is present and instructions match the exported content. Tags, licence and run settings (model, max tokens, reasoning effort) are restored |
| 7 | Save the imported Skill | Skill saves without errors; no validation or save errors are shown |

---

## Expected Final State

A new Skill exists in the system with a unique ID, a `base` version, and all fields (name, description, tags, licence, run settings, instructions) correctly populated from the imported `.md` file.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Imported Skill has a unique ID, `base` version is present, and all fields are correctly populated.

**Fail:**
- Any step produces an error or unexpected result.
- The exported file is not `.md`, missing required fields, the imported Skill ID duplicates the source, or the Skill cannot be saved after import.
