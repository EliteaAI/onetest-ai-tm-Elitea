---
id: ELITEA-3758
title: Export Agent with Non-Empty Editor Notes - Verify Field Included in Export File
module: Agent Management
feature: Agent Export
priority: critical
status: draft
tags:
  - feat:agents
  - eng:export
  - editor-notes
  - EL-6156
related_issue: https://github.com/EliteaAI/elitea_issues/issues/6156
acceptance_criteria: AC1 - Export: Editor Notes Included in Exported File
---

## Test Case Summary

Verify that when an agent with a non-empty Editor Notes field is exported, the exported `.md` file includes a `notes` field with the correct value positioned consistently alongside other metadata fields.

## Preconditions

- User is logged into ELITEA platform at https://next.elitea.ai/app/
- User has access to Private project
- At least one agent exists with non-empty Editor Notes field
- User has permission to export agents

## Test Data

| Field | Value |
|-------|-------|
| Agent Name | QA Test Agent - Export Notes |
| Editor Notes | "This is a test note for QA validation" |

## Test Steps

| Step | Action | Expected Result |
|------|--------|----------------|
| 1 | Navigate to Agents page in Private project | Agents list page loads successfully |
| 2 | Open the test agent "QA Test Agent - Export Notes" | Agent details page displays |
| 3 | Scroll down to locate Editor Notes section | Editor Notes section visible |
| 4 | Verify Editor Notes field contains test value | Field displays: "This is a test note for QA validation" |
| 5 | Click on agent menu icon (⋮) in top-right corner | Dropdown menu opens showing options |
| 6 | Click "Export" option from dropdown | Export action triggered |
| 7 | Verify file download initiated | Browser shows download progress/notification |
| 8 | Check downloads folder for exported file | File `qa-test-agent-export-notes.md` (or similar) downloaded |
| 9 | Open the downloaded `.md` file in a text editor | File opens without errors |
| 10 | Locate the frontmatter/metadata section at top of file | YAML frontmatter block found (between `---` markers) |
| 11 | Search for "notes" field in metadata section | `notes` field found in metadata |
| 12 | Verify notes field value matches original | Value is: `notes: "This is a test note for QA validation"` |
| 13 | Verify notes field placement | Field positioned alongside other metadata: `model`, `step_limit`, `welcome_message`, `instructions` |
| 14 | Verify field formatting | Proper YAML formatting with correct indentation |

## Expected Results

- ✅ Export completes successfully
- ✅ Downloaded `.md` file contains `notes` field in frontmatter
- ✅ `notes` field value matches Editor Notes from UI: "This is a test note for QA validation"
- ✅ `notes` field positioned consistently with other metadata fields
- ✅ Proper YAML formatting applied

## Actual Results

_(To be filled during test execution)_

## Pass/Fail Criteria

**PASS:** All steps execute successfully and notes field is present with correct value in exported file

**FAIL:** Any of the following:
- Export fails or file not downloaded
- `notes` field missing from exported file
- `notes` value incorrect or corrupted
- Improper formatting or placement

## Notes

- This test validates AC1 from issue EL-6156
- Linked PR: elitea_core #315, EliteaUI #749
- Export format may vary (YAML frontmatter vs JSON) - verify correct format for platform

