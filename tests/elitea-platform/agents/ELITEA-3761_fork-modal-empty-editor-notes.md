---
id: ELITEA-3761
title: Fork Modal - Verify Empty Editor Notes Section Displayed But Empty
module: Agent Management
feature: Agent Fork
priority: critical
status: draft
tags:
  - feat:agents
  - eng:fork
  - editor-notes
  - edge-case
  - ui
  - EL-6156
related_issue: https://github.com/EliteaAI/elitea_issues/issues/6156
acceptance_criteria: AC2 - If notes field is empty or null, section should be empty
---

## Test Case Summary

Verify that when forking an agent with an empty or null Editor Notes field, the Fork Parameters modal displays the "EDITOR NOTES:" section header, but the content area is empty (section is not hidden entirely).

## Preconditions

- User is logged into ELITEA platform at https://next.elitea.ai/app/
- User has access to Private project
- At least one agent exists with empty/null Editor Notes field
- User has permission to fork agents

## Test Data

| Field | Value |
|-------|-------|
| Source Agent Name | QA Source Agent - Empty Notes Fork |
| Editor Notes | (empty/null) |

## Test Steps

| Step | Action | Expected Result |
|------|--------|----------------|
| 1 | Navigate to Agents page in Private project | Agents list page loads |
| 2 | Open or create agent with empty Editor Notes | Agent details page displays |
| 3 | Verify Editor Notes field is empty | Field blank or shows placeholder |
| 4 | Save agent (if newly created) | Agent saved successfully |
| 5 | Click agent menu (⋮) → Fork | Fork Parameters modal opens |
| 6 | Click "Show details" (if collapsed) | Details section expands |
| 7 | Scroll through all modal sections | All sections visible |
| 8 | Locate "EDITOR NOTES:" section | Section header found |
| 9 | Verify section header is visible | "EDITOR NOTES:" text displayed |
| 10 | Check content area below header | Content area visible but empty |
| 11 | Verify no content displayed | No text, no placeholder like "(empty)" or "None" |
| 12 | Verify section is not hidden/removed | Section remains in DOM (inspect element confirms) |
| 13 | Compare to other empty sections | Same behavior as other empty sections (if any) |
| 14 | Verify section ordering | EDITOR NOTES in expected position relative to other sections |
| 15 | Verify vertical spacing | Spacing consistent even when empty |

## Expected Results

- ✅ Fork Parameters modal opens successfully
- ✅ "EDITOR NOTES:" section header visible
- ✅ Content area empty (no text displayed)
- ✅ Section not hidden or removed from modal
- ✅ Consistent vertical spacing maintained
- ✅ No visual artifacts or layout issues

## Actual Results

_(To be filled during test execution)_

## Pass/Fail Criteria

**PASS:** All steps execute successfully, section header visible but content area empty

**FAIL:** Any of the following:
- EDITOR NOTES section completely hidden when empty
- Displays incorrect placeholder text (e.g., literal "null" or "undefined")
- Layout broken or collapsed
- Inconsistent with other empty sections in modal

## Notes

- This test validates AC2 empty/null handling in Fork modal
- Section should be visible but empty, not removed from UI
- Verify behavior matches platform's pattern for other empty sections
- Take screenshot for documentation

