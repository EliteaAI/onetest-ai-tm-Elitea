---
id: ELITEA-1795
title: "Import Agent with attached Skills recreates Skills with new IDs"
priority: high
type: functional
module: skills
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:skills]
requirements: []
---

# ELITEA-1795: Import Agent with attached Skills recreates Skills with new IDs

**Module:** skills · **Priority:** high · **Type:** functional

**Objective:** Verify that importing an Agent `.md` file that contains embedded Skill content creates new Skill entries with unique IDs in the target project, and that the imported Agent is correctly linked to the newly created Skills.

---

## Preconditions

- User is logged in to the Elitea platform.
- A project exists and is accessible.
- The Skills and Agents sections are available in the project.
- An Agent `.md` export file is available that was previously exported from an Agent with at least one attached Skill (see ELITEA-1794).
- The Agent import feature is available.

---

## Test Data

| Field | Value |
|-------|-------|
| Import file | Agent `.md` export containing embedded Skill content |
| Source Agent name | (e.g., "Export Test Agent") |
| Source Skill name | (e.g., "Formatter") |
| Expected behavior | New Skill created with a new unique ID; Agent linked to the new Skill |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Agents and trigger the Import action | Import dialog or file picker is shown |
| 2 | Select the previously exported Agent `.md` file and confirm the import | Import process completes without errors |
| 3 | Verify the imported Agent appears in the Agents list | A new Agent entry is present; its name matches the exported Agent |
| 4 | Open the imported Agent and inspect the attached Skills | The Skill from the original export is listed as attached to the imported Agent |
| 5 | Navigate to the Skills section and locate the newly created Skill | A new Skill entry exists with the same name as the original Skill |
| 6 | Verify the newly created Skill has a new unique ID different from any original Skill ID | The new Skill's ID is different from the source Skill's ID |
| 7 | Verify the new Skill's instructions and content match the exported content | Skill instructions are correctly populated from the import |
| 8 | Verify the imported Agent can be saved or used without errors | Agent is functional and saves without errors |

---

## Expected Final State

The import process creates a new Agent and new Skill entries (with unique IDs) in the target project. The imported Agent is linked to the newly created Skills. Original Skills are unaffected. The new Skills contain all content from the exported file.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Imported Agent appears with the Skill attached.
- New Skill is created with a unique ID distinct from any original.
- Skill instructions match the exported content.

**Fail:**
- Any step produces an error or unexpected result.
- No new Skill is created (import only links to existing Skills by ID).
- The new Skill ID duplicates the source Skill's ID.
- Skill content is missing or incorrectly imported.
