---
id: ELITEA-0147
title: Export Agent with Empty/Null Editor Notes - Verify Null Field in Export File
module: Agent Management
feature: Agent Export
priority: critical
status: draft
tags:
  - feat:agents
  - eng:export
  - editor-notes
  - edge-case
  - EL-6156
related_issue: https://github.com/EliteaAI/elitea_issues/issues/6156
acceptance_criteria: AC1 - If notes field is empty or null, should be showed as null
---

## Test Case Summary

Verify that when an agent with an empty or null Editor Notes field is exported, the exported `.md` file includes a `notes` field with `null` value (not omitted entirely), and that re-importing creates an empty Editor Notes field.

## Preconditions

- User is logged into ELITEA platform at https://next.elitea.ai/app/
- User has access to Private project
- At least one agent exists with empty/null Editor Notes field
- User has permission to export and import agents

## Test Data

| Field | Value |
|-------|-------|
| Agent Name | QA Test Agent - Empty Notes |
| Editor Notes | (empty/null) |

## Test Steps

| Step | Action | Expected Result |
|------|--------|----------------|
| 1 | Navigate to Agents page in Private project | Agents list page loads |
| 2 | Create new agent or open existing agent with no Editor Notes | Agent details page displays |
| 3 | Scroll to Editor Notes section | Section visible |
| 4 | Verify Editor Notes field is empty | Field contains no text or shows placeholder |
| 5 | Click Save (if creating new agent) | Agent saved successfully |
| 6 | Click agent menu (⋮) → Export | Export option visible |
| 7 | Click Export | File downloads |
| 8 | Open downloaded `.md` file in text editor | File opens successfully |
| 9 | Locate frontmatter/metadata section | Metadata block found |
| 10 | Search for "notes" field | `notes` field present in metadata |
| 11 | Verify notes field value | Value is `notes: null` or `notes: ""` (consistent with platform convention) |
| 12 | Verify field is not omitted | `notes` field explicitly included (not missing) |
| 13 | Compare with other null/empty fields | Same null representation used (e.g., `welcome_message: null`) |
| 14 | Save exported file for re-import test | File saved |
| 15 | Navigate to Agents page | Page loads |
| 16 | Click Import Agent (or equivalent action) | Import dialog opens |
| 17 | Select the exported `.md` file with null notes | File selected |
| 18 | Complete import process | Import succeeds, new agent created |
| 19 | Open imported agent details | Agent page loads |
| 20 | Verify Editor Notes field | Field is empty/unpopulated (not containing literal "null" text) |

## Expected Results

- ✅ Export completes successfully
- ✅ Exported file contains `notes: null` or equivalent empty representation
- ✅ `notes` field not omitted from export (explicitly included)
- ✅ Null representation consistent with other empty fields
- ✅ Re-imported agent has empty Editor Notes field (not literal "null" text)

## Actual Results

_(To be filled during test execution)_

## Pass/Fail Criteria

**PASS:** All steps execute successfully, notes field present as null in export, and re-import creates empty field

**FAIL:** Any of the following:
- `notes` field omitted from export when empty
- `notes` field contains incorrect value (not null/empty)
- Re-imported agent shows literal "null" text instead of empty field
- Inconsistent null handling compared to other fields

## Notes

- This test validates AC1 empty/null handling requirement
- Critical for ensuring data consistency in export/import cycle
- Verify platform's null representation convention (YAML null, empty string, etc.)

