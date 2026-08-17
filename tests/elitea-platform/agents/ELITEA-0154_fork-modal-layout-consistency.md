---
id: ELITEA-0154
title: Fork Modal - Verify Editor Notes Section Layout Consistency with Other Sections
module: Agent Management
feature: Agent Fork
priority: high
status: draft
tags:
  - feat:agents
  - eng:fork
  - editor-notes
  - ui
  - visual-consistency
  - EL-6156
related_issue: https://github.com/EliteaAI/elitea_issues/issues/6156
acceptance_criteria: AC2 - Visual/layout pattern matches other sections
---

## Test Case Summary

Verify that the EDITOR NOTES section in the Fork Parameters modal follows the same visual and layout patterns as other existing sections (DESCRIPTION, INSTRUCTIONS, WELCOME MESSAGE, CHAT STARTERS, OTHER).

## Preconditions

- User is logged into ELITEA platform at https://next.elitea.ai/app/
- User has access to Private project
- At least one agent exists with populated Editor Notes and other fields
- User has permission to fork agents

## Test Data

| Field | Value |
|-------|-------|
| Source Agent Name | QA Agent - Layout Consistency Test |
| Description | (populated) |
| Instructions | (populated) |
| Welcome Message | (populated) |
| Chat Starters | (populated) |
| Editor Notes | "Layout consistency check" |

## Test Steps

| Step | Action | Expected Result | Visual Check |
|------|--------|----------------|--------------|
| 1 | Navigate to Agents page | Page loads | - |
| 2 | Open source agent with all fields populated | Agent page displays | - |
| 3 | Click Fork from agent menu | Fork Parameters modal opens | - |
| 4 | Click "Show details" | Details section expands | - |
| 5 | Locate DESCRIPTION section | Section visible | Note header styling |
| 6 | Locate EDITOR NOTES section | Section visible | Compare to DESCRIPTION |
| 7 | Compare section header font | Both sections | ✅ Same font family |
| 8 | Compare section header size | Both sections | ✅ Same font size |
| 9 | Compare section header color | Both sections | ✅ Same text color |
| 10 | Compare section header case | Both sections | ✅ Both uppercase |
| 11 | Locate INSTRUCTIONS section | Section visible | - |
| 12 | Check for expand/collapse icon (⤢) on INSTRUCTIONS | Icon present/absent | Note state |
| 13 | Check for expand/collapse icon on EDITOR NOTES | Icon present/absent | ✅ Match INSTRUCTIONS behavior |
| 14 | Locate WELCOME MESSAGE section | Section visible | Note content box styling |
| 15 | Compare content box background color | WELCOME MESSAGE vs EDITOR NOTES | ✅ Same background |
| 16 | Compare content box padding | WELCOME MESSAGE vs EDITOR NOTES | ✅ Same padding |
| 17 | Compare content box border | WELCOME MESSAGE vs EDITOR NOTES | ✅ Same border style |
| 18 | Compare content box border-radius | WELCOME MESSAGE vs EDITOR NOTES | ✅ Same corner radius |
| 19 | Locate CHAT STARTERS section | Section visible | - |
| 20 | Measure vertical spacing above CHAT STARTERS | Note spacing | Record value |
| 21 | Measure vertical spacing above EDITOR NOTES | Note spacing | ✅ Same as CHAT STARTERS |
| 22 | Measure vertical spacing below EDITOR NOTES | Note spacing | ✅ Consistent with pattern |
| 23 | Test expand/collapse on INSTRUCTIONS (if applicable) | Click header | Note animation/behavior |
| 24 | Test expand/collapse on EDITOR NOTES (if applicable) | Click header | ✅ Same animation/behavior |
| 25 | Verify horizontal alignment | All sections | ✅ All headers left-aligned consistently |

## Expected Results

**Header Styling:**
- ✅ Font family matches other sections
- ✅ Font size matches other sections
- ✅ Color matches other sections
- ✅ Uppercase formatting consistent

**Content Box Styling:**
- ✅ Background color matches
- ✅ Padding matches
- ✅ Border style matches
- ✅ Border radius matches

**Spacing:**
- ✅ Vertical spacing above section consistent
- ✅ Vertical spacing below section consistent
- ✅ Horizontal alignment consistent

**Interactive Behavior:**
- ✅ Expand/collapse icon present if other sections have it
- ✅ Expand/collapse behavior matches other sections

## Actual Results

_(To be filled during test execution - include screenshots)_

## Pass/Fail Criteria

**PASS:** EDITOR NOTES section visual styling and layout is indistinguishable from other sections' pattern

**FAIL:** Any visual inconsistency:
- Header styling differs
- Content box styling differs
- Spacing inconsistent
- Interactive behavior different
- Any layout anomaly

## Notes

- Use browser DevTools to inspect CSS properties for precise comparison
- Take screenshots of modal showing multiple sections for documentation
- Compare against reference screenshots from issue #6156
- Visual consistency is critical for UI/UX quality

