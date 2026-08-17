---
id: ELITEA-0148
title: Fork Modal - Verify Non-Empty Editor Notes Displayed in Fork Parameters Preview
module: Agent Management
feature: Agent Fork
priority: critical
status: draft
tags:
  - feat:agents
  - eng:fork
  - editor-notes
  - ui
  - EL-6156
related_issue: https://github.com/EliteaAI/elitea_issues/issues/6156
acceptance_criteria: AC2 - Fork Modal: Editor Notes Displayed in Fork Parameters Preview
---

## Test Case Summary

Verify that when forking an agent with a non-empty Editor Notes field, the Fork Parameters modal displays an "EDITOR NOTES:" section showing the notes content with visual/layout consistency matching other modal sections.

## Preconditions

- User is logged into ELITEA platform at https://next.elitea.ai/app/
- User has access to Private project
- At least one agent exists with non-empty Editor Notes field
- User has permission to fork agents

## Test Data

| Field | Value |
|-------|-------|
| Source Agent Name | QA Source Agent - Fork Test |
| Editor Notes | "Source agent notes for forking test" |

## Test Steps

| Step | Action | Expected Result |
|------|--------|----------------|
| 1 | Navigate to Agents page in Private project | Agents list page loads |
| 2 | Open source agent "QA Source Agent - Fork Test" | Agent details page displays |
| 3 | Scroll to Editor Notes section | Section visible |
| 4 | Verify Editor Notes contains test value | Field shows: "Source agent notes for forking test" |
| 5 | Click agent menu icon (⋮) in top-right | Dropdown menu opens |
| 6 | Click "Fork" option from menu | Fork Parameters modal opens |
| 7 | Verify modal header displays "Fork parameters" | Modal header correct |
| 8 | Locate "Show details" / "Hide details" link | Link visible in modal |
| 9 | Click "Show details" (if details collapsed) | Details section expands |
| 10 | Scroll through modal sections | Multiple sections visible |
| 11 | Verify standard sections present | Sections: DESCRIPTION, INSTRUCTIONS, WELCOME MESSAGE, CHAT STARTERS, OTHER |
| 12 | Locate "EDITOR NOTES:" section | Section header found in modal |
| 13 | Verify EDITOR NOTES section header styling | Header matches other sections (same font, size, uppercase) |
| 14 | Verify Editor Notes content displayed | Content shows: "Source agent notes for forking test" |
| 15 | Verify content box styling | Same background color, padding, border as other sections |
| 16 | Check for expand/collapse icon (⤢) | Icon present if applicable (consistent with other sections) |
| 17 | Verify vertical spacing | Spacing between EDITOR NOTES and adjacent sections is consistent |
| 18 | Test expand/collapse (if supported) | Clicking expands/collapses correctly |
| 19 | Compare to WELCOME MESSAGE section | Same visual pattern/layout |
| 20 | Compare to CHAT STARTERS section | Same visual pattern/layout |

## Expected Results

- ✅ Fork Parameters modal opens successfully
- ✅ "EDITOR NOTES:" section visible in modal
- ✅ Editor Notes content displays: "Source agent notes for forking test"
- ✅ Section header styling matches other sections (DESCRIPTION, INSTRUCTIONS, etc.)
- ✅ Content box styling consistent with other sections
- ✅ Vertical spacing consistent
- ✅ Expand/collapse behavior (if applicable) works correctly
- ✅ Overall visual consistency with modal's design pattern

## Actual Results

_(To be filled during test execution)_

## Pass/Fail Criteria

**PASS:** All steps execute successfully and EDITOR NOTES section is visible with correct styling and content

**FAIL:** Any of the following:
- Fork modal fails to open
- EDITOR NOTES section missing from modal
- Content incorrect or not displayed
- Visual inconsistency with other sections (styling, spacing, behavior)
- Layout broken or content overflow

## Notes

- This test validates AC2 UI display requirement
- Compare screenshots with other sections to verify visual consistency
- Linked PR: EliteaUI #749
- Take screenshot of modal showing EDITOR NOTES section for documentation

