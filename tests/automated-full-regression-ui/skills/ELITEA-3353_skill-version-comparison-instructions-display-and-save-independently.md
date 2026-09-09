---
id: ELITEA-3353
title: "Skill Version Comparison Displays Instructions and Saves Independently"
priority: critical
type: regression
module: skills
status: draft
execution_type: manual
tags: [feat:skills, r-2.0.6, regression, version-comparison, data-integrity, story:6304]
requirements: [EliteaAI/elitea_issues#6304]
---
# ELITEA-3353: Skill Version Comparison Displays Instructions and Saves Independently

**Module:** Skills · **Priority:** Critical · **Type:** Regression

**Objective:** Verifies that the Instructions section displays correctly in the skill comparison modal, and that saving changes to one version does not affect the other version.

## Preconditions

- User is logged in to `{{base_url}}` with edit permissions
- Test skill exists with 2+ versions containing different Instructions text

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/skills` |
| Test Skill | Skill with 2+ versions |
| Version 1 | base - Instructions: "Base skill instructions for data processing" |
| Version 2 | v1.0 - Instructions: "V1.0 skill instructions with advanced data processing" |
| Version 1 Edit | "Updated base skill instructions" |
| Version 2 Edit | "Updated v1.0 skill instructions" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open Compare Versions modal for test skill | Modal opens with both versions displayed |
| 2 | Verify **Instructions** section is displayed | Instructions section visible with section header |
| 3 | Verify Instructions shows editable text areas for both versions | Two text areas visible side-by-side; both are editable |
| 4 | Verify Version 1 displays original instructions: "Base skill instructions for data processing" | Correct content displayed for Version 1 |
| 5 | Verify Version 2 displays original instructions: "V1.0 skill instructions with advanced data processing" | Correct content displayed for Version 2 |
| 6 | Verify NO other sections are displayed (Skills only have Instructions section) | Only Instructions section visible; no User Interaction or Tools & Skills sections |
| 7 | Edit Instructions in Version 1 (left column) to "Updated base skill instructions" | Text updates in Version 1 column only |
| 8 | Verify Version 2 (right column) Instructions remains unchanged | Version 2 still shows original instructions |
| 9 | Click Save button for Version 1 column | Save operation executes; success message or indicator appears |
| 10 | Verify Version 1 Instructions field shows saved changes | Version 1 displays "Updated base skill instructions" |
| 11 | Close the Compare Versions modal | Modal closes |
| 12 | Reopen Compare Versions modal for same skill | Modal reopens with fresh data |
| 13 | Verify Version 1 Instructions shows saved changes: "Updated base skill instructions" | Version 1 displays the updated text |
| 14 | Verify Version 2 Instructions remains unchanged from original | Version 2 was not affected by Version 1 save |
| 15 | Edit Instructions in Version 2 to "Updated v1.0 skill instructions" | Text updates in Version 2 column only |
| 16 | Click Save button for Version 2 column | Save operation executes; success message appears |
| 17 | Close and reopen modal | Modal reopens |
| 18 | Verify Version 2 now shows "Updated v1.0 skill instructions" | Version 2 displays saved changes |
| 19 | Verify Version 1 still shows "Updated base skill instructions" (unchanged by Version 2 save) | Version 1 unaffected by Version 2 save |
| 20 | Verify both versions persist their individual changes | Both versions show their respective saved changes |

## Expected Final State

Instructions section displays correctly with content from both versions. Saving changes to one version does not affect the other version. Changes persist after modal close/reopen.

## Pass/Fail Criteria

**Pass:**
- Instructions section displays with editable text areas
- Both skill versions show their original instructions correctly
- Only Instructions section visible (no other sections for Skills)
- Content from both versions visible side-by-side
- Saving Version 1 does not modify Version 2
- Saving Version 2 does not modify Version 1
- Saved changes persist after closing and reopening modal
- Text areas are editable (not read-only)

**Fail:**
- Instructions section is missing or fails to load
- Content from only one version is visible
- Other sections are incorrectly displayed (Skills should only have Instructions)
- Saving one version affects the other version
- Changes do not persist after modal close/reopen
- Save button saves both versions instead of only the clicked version
- Text areas are read-only when they should be editable
