---
id: ELITEA-0650
title: "Import Widget Correctly Groups Toolkits/MCPs Into \"Imported\" and \"Ignored\" Lists on Name Conflict"
priority: medium
type: functional
module: export-import
status: draft
execution_type: manual
tags: [feat:import-forking, user_story:3343, r-2.0.2]
requirements: [ProjectAlita/projectalita.github.io#3791]
---
# ELITEA-0650: Import Widget Correctly Groups Toolkits/MCPs Into "Imported" and "Ignored" Lists on Name Conflict

**Module:** Export Import · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that when importing an agent/pipeline whose referenced Toolkits/MCPs already exist in the destination project, the Import widget displays two separate groups — "Imported" and "Ignored" — rather than a false 100% success.

**Coverage:**
- Toolkits/MCPs with name conflicts appear in the "Ignored" group
- Toolkits/MCPs without conflicts appear in the "Imported" group
- The import summary is not falsely reported as 100% success when items are ignored

## Preconditions

- Access to project **"Bugs & Features"**
- At least one **Toolkit** and/or **MCP** already exists in the destination project ("Bugs & Features") with a known name (e.g., `existing-toolkit`, `existing-mcp`)
- A pipeline or agent `.md` file is prepared that references at least one Toolkit/MCP whose name **already exists in the destination project** ("Bugs & Features"), AND at least one Toolkit/MCP whose name does **not yet exist** in that project
- Browser: Chrome latest

## Test Data

- Project: `Bugs & Features`
- Import file: `pipeline-to-import.md` (attached to GitHub issue #3791)
- Conflicting name: name of a Toolkit/MCP already present in the destination project
- New name: a Toolkit/MCP name not yet present in the destination project

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Pipelines (`/app/pipelines/all`). Click the Import button and upload `pipeline-to-import.md`. | File is accepted. Import processing starts. |
| 2 | Wait for import to complete. Observe the Import widget summary without navigating away. | Widget displays two groups: **"Imported"** (new Toolkits/MCPs that were created) and **"Ignored"** (ones already existing in the project by name). |
| 3 | Check the **"Ignored"** group in the import summary. | The group lists the Toolkits/MCPs that were skipped because they already exist in the destination project by name. |
| 4 | Check the **"Imported"** group in the import summary. | The group lists only the Toolkits/MCPs that were actually newly created. |
| 5 | Navigate to the project's Toolkits and MCPs lists. | No duplicate entries were created. Existing items are unchanged. Newly imported items are present. |

## Expected Final State

No duplicate entries were created. Existing items are unchanged. Newly imported items are present.

## Pass/Fail Criteria

**Pass:**
- Import widget shows both "Imported" and "Ignored" groups with correct items in each
- No conflicting Toolkit/MCP appears in the "Imported" group
- Existing Toolkits/MCPs in the destination project are not duplicated or overwritten

**Fail:**
- Widget shows 100% success with no distinction between imported and ignored items
- Conflicting items are silently skipped with no visibility in the summary
- Duplicates are created or existing items are overwritten
