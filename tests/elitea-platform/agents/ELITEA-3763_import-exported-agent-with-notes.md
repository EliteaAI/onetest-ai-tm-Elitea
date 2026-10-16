---
id: ELITEA-3763
title: Import Agent - Verify Re-importing Exported Agent Populates Editor Notes
module: Agent Management
feature: Agent Import
priority: high
status: draft
tags:
  - feat:agents
  - eng:import
  - editor-notes
  - EL-6156
related_issue: https://github.com/EliteaAI/elitea_issues/issues/6156
acceptance_criteria: AC1 - Re-importing with notes field populates Editor Notes
---

## Test Case Summary

Verify that re-importing an exported agent `.md` file that contains a `notes` field correctly populates the Editor Notes section in the newly imported agent.

## Preconditions

- User is logged into ELITEA platform at https://next.elitea.ai/app/
- User has access to Private project
- User has a previously exported `.md` file containing `notes: "Reimport test value"`
- User has permission to import agents

## Test Data

**Exported File Content (excerpt):**
```yaml
---
name: QA Import Test Agent
model: gpt-5.4-mini
notes: "Reimport test value"
...
---
```

## Test Steps

| Step | Action | Expected Result |
|------|--------|----------------|
| 1 | Navigate to Agents page in Private project | Agents list page loads |
| 2 | Locate "Import Agent" button or equivalent action | Button visible (may be in menu or toolbar) |
| 3 | Click "Import Agent" | Import dialog/modal opens |
| 4 | Click "Choose file" or drag-and-drop area | File picker opens |
| 5 | Select the exported `.md` file with notes field | File selected, name displayed in dialog |
| 6 | Verify file name displayed | Shows selected file name (e.g., "qa-import-test-agent.md") |
| 7 | Click "Import" or "Upload" button | Import process starts |
| 8 | Wait for import to complete | Progress indicator shown then completes |
| 9 | Verify success message or notification | Message shows "Agent imported successfully" or similar |
| 10 | Verify navigation to imported agent page | Browser navigates to new agent details page |
| 11 | Check agent name matches imported file | Name is "QA Import Test Agent" |
| 12 | Scroll through agent configuration | All sections visible |
| 13 | Locate Editor Notes section | Section found below other fields |
| 14 | Verify Editor Notes field is populated | Field contains text (not empty) |
| 15 | Verify Editor Notes value | Value is: "Reimport test value" |
| 16 | Verify exact match with exported file | Character-by-character match |
| 17 | Open exported file in text editor | File opens |
| 18 | Compare notes value in file vs UI | Values match exactly |

## Expected Results

- ✅ Import process completes successfully
- ✅ New agent created from imported file
- ✅ Editor Notes field populated in imported agent
- ✅ Editor Notes value matches file: "Reimport test value"
- ✅ No data loss or corruption during import

## Actual Results

_(To be filled during test execution)_

## Pass/Fail Criteria

**PASS:** All steps execute successfully and imported agent's Editor Notes matches exported file value

**FAIL:** Any of the following:
- Import fails or errors
- Editor Notes field empty after import
- Editor Notes value incorrect, truncated, or corrupted
- Import succeeds but notes field ignored

## Notes

- This test validates AC1 re-import requirement
- Completes the export → import cycle
- Verifies no data loss in round-trip
- Prepare test file by exporting agent with known notes value first

