---
id: ELITEA-0153
title: Export and Import - Verify Long Editor Notes Content (>1000 chars) Preserved
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

Verify that Editor Notes containing long content (~1500 characters) is fully exported without truncation and correctly preserved through the export → import cycle.

## Preconditions

- User is logged into ELITEA platform at https://next.elitea.ai/app/
- User has access to Private project
- User has permission to create, export, and import agents

## Test Data

| Field | Value |
|-------|-------|
| Agent Name | QA Test Agent - Long Notes |
| Editor Notes | (1500 character string - see below) |

**Editor Notes Content (1500 chars):**
```
This is a comprehensive test of long-form Editor Notes content to verify that the export and import functionality handles large text blocks without truncation, corruption, or data loss. This content is designed to exceed typical short note lengths and simulate real-world scenarios where developers or QA engineers might include detailed documentation, background context, implementation notes, troubleshooting steps, or comprehensive testing instructions directly within the agent's metadata. The content should flow naturally through multiple sentences and paragraphs to test line break handling, spacing preservation, and overall text integrity throughout the export-import lifecycle. Additional filler text to reach approximately 1500 characters: Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum. Testing complete at 1500 characters approximately.
```

## Test Steps

| Step | Action | Expected Result |
|------|--------|----------------|
| 1 | Navigate to Agents page | Page loads |
| 2 | Create new agent "QA Test Agent - Long Notes" | Agent created |
| 3 | Copy 1500-character test content | Content copied to clipboard |
| 4 | Paste into Editor Notes field | Content pasted successfully |
| 5 | Verify entire content visible in UI (scroll within field if needed) | All 1500 characters visible, no truncation warning |
| 6 | Count characters or verify length indicator (if available) | Shows ~1500 characters |
| 7 | Click Save | Agent saved successfully |
| 8 | Reload agent page | Page reloads |
| 9 | Verify Editor Notes still shows full content | All content present after page refresh |
| 10 | Export agent to `.md` file | Export succeeds |
| 11 | Open exported file in text editor | File opens |
| 12 | Locate notes field | Field found |
| 13 | Select/copy notes field value | Value copied |
| 14 | Paste into character counter tool or text editor | Content pasted |
| 15 | Verify character count | Count is ~1500 (full content present) |
| 16 | Verify no truncation markers (e.g., "...") | No truncation in exported file |
| 17 | Close and save exported file | File saved |
| 18 | Import exported file back into platform | Import succeeds |
| 19 | Open imported agent | Agent page loads |
| 20 | Verify Editor Notes field populated | Field contains long content |
| 21 | Copy imported Editor Notes content | Content copied |
| 22 | Compare original vs imported (diff tool or manual) | Exact match, all 1500 characters preserved |

## Expected Results

- ✅ UI accepts and displays long Editor Notes content without truncation
- ✅ Save succeeds with long content
- ✅ Export includes full 1500 characters in notes field
- ✅ No truncation in exported file
- ✅ Import succeeds with long content
- ✅ Imported agent contains all 1500 characters
- ✅ No data loss throughout cycle

## Actual Results

_(To be filled during test execution)_

## Pass/Fail Criteria

**PASS:** All 1500 characters preserved through save → export → import cycle with no truncation or data loss

**FAIL:** Any of the following:
- UI truncates content on save
- Export truncates notes field
- Character count mismatch in exported file
- Import fails or truncates content
- Any data loss detected

## Notes

- Tests platform's handling of large text fields
- Verify no hardcoded length limits in export/import logic
- 1500 characters is representative; adjust if platform has documented limits
- Consider testing even longer content (5000+ chars) if this test passes

