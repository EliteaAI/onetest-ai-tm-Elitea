---
id: ELITEA-3764
title: Export and Import - Verify Special Characters Preserved in Editor Notes
module: Agent Management
feature: Agent Export, Agent Import
priority: high
status: draft
tags:
  - feat:agents
  - eng:export
  - eng:import
  - editor-notes
  - edge-case
  - EL-6156
related_issue: https://github.com/EliteaAI/elitea_issues/issues/6156
---

## Test Case Summary

Verify that Editor Notes containing special characters (quotes, double quotes, line breaks, symbols) are properly escaped/encoded during export and correctly preserved through the export → import cycle.

## Preconditions

- User is logged into ELITEA platform at https://next.elitea.ai/app/
- User has access to Private project
- User has permission to create, export, and import agents

## Test Data

| Field | Value |
|-------|-------|
| Agent Name | QA Test Agent - Special Chars |
| Editor Notes | `Test with 'single quotes', "double quotes", line\nbreaks, & ampersand, < > symbols, #hashtag, @mention` |

## Test Steps

| Step | Action | Expected Result |
|------|--------|----------------|
| 1 | Navigate to Agents page | Page loads |
| 2 | Create new agent "QA Test Agent - Special Chars" | Agent created |
| 3 | In Editor Notes field, enter test data with special characters | Text entered successfully |
| 4 | Click Save | Agent saved without errors |
| 5 | Verify Editor Notes displays correctly in UI | All special characters visible correctly |
| 6 | Export agent to `.md` file | File downloads successfully |
| 7 | Open exported file in text editor | File opens |
| 8 | Locate notes field in metadata | Field found |
| 9 | Verify special characters escaped/encoded properly | Characters properly escaped (e.g., YAML string escaping: `"Test with 'single quotes', \"double quotes\"..."`) |
| 10 | Verify file syntax is valid | No YAML/Markdown parsing errors |
| 11 | Verify line breaks encoded correctly | Line breaks as `\n` or YAML multiline format |
| 12 | Save exported file | File saved |
| 13 | Navigate to Agents page | Page loads |
| 14 | Import the exported file | Import succeeds |
| 15 | Open imported agent | Agent page loads |
| 16 | Locate Editor Notes field | Field visible |
| 17 | Verify all special characters preserved | Content matches original: single quotes, double quotes, line breaks, symbols all present |
| 18 | Compare original vs imported character-by-character | Exact match (or semantically equivalent for line breaks) |

## Expected Results

- ✅ Agent saves successfully with special characters
- ✅ Export completes without errors
- ✅ Exported file has proper escaping/encoding
- ✅ Exported file is valid YAML/Markdown (no parse errors)
- ✅ Import succeeds
- ✅ All special characters preserved in imported agent
- ✅ No data corruption or loss

## Actual Results

_(To be filled during test execution)_

## Pass/Fail Criteria

**PASS:** All special characters correctly handled through export → import cycle with no data loss

**FAIL:** Any of the following:
- Save fails with special characters
- Export fails or produces invalid file
- Special characters corrupted, escaped incorrectly, or lost
- Import fails or produces incorrect Editor Notes value
- Any character mismatch between original and imported

## Notes

- Tests robustness of export/import with edge-case input
- Platform should handle YAML string escaping automatically
- Line breaks may be represented differently (\n vs actual breaks) but should be semantically equivalent
- Consider testing additional special characters: tabs, unicode, emoji in separate test

