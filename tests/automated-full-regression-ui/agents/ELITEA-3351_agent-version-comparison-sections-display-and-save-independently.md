---
id: ELITEA-3351
title: "Agent Version Comparison Displays All Sections and Saves Independently"
priority: critical
type: regression
module: agents
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.6, regression, version-comparison, data-integrity, story:6304]
requirements: [EliteaAI/elitea_issues#6304]
---
# ELITEA-3351: Agent Version Comparison Displays All Sections and Saves Independently

**Module:** Agents · **Priority:** Critical · **Type:** Regression

**Objective:** Verifies that all agent sections (Instructions, User Interaction, Tools & Skills) display correctly in the comparison modal, and that saving changes to one version does not affect the other version.

## Preconditions

- User is logged in to `{{base_url}}` with edit permissions
- Test agent exists with 2+ versions containing different configurations:
  - Different Instructions text
  - Different Welcome Messages
  - Different Chat Starters
  - Different Tools/Skills attached (optional for basic test)

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/agents` |
| Test Agent | Agent with complete configuration across 2 versions |
| Version 1 | base - Instructions: "Base version instructions", Welcome: "Base welcome" |
| Version 2 | v1.0 - Instructions: "V1 instructions", Welcome: "V1 welcome" |
| Version 1 Edit | "Updated base instructions" |
| Version 2 Edit | "Updated v1.0 instructions" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open Compare Versions modal for test agent | Modal opens with both versions displayed |
| 2 | Verify **Instructions** section is displayed | Instructions section visible with header |
| 3 | Verify Instructions shows text areas for both versions with different content | Two text areas visible side-by-side; content differs between versions |
| 4 | Navigate to **User Interaction** section (if wizard/tabs present) | User Interaction section loads successfully |
| 5 | Verify Welcome Message fields are displayed for both versions | Welcome Message text areas visible for both versions |
| 6 | Verify Chat Starters section is displayed (if applicable) | Chat Starters fields visible |
| 7 | Navigate to **Tools & Skills** section (if wizard/tabs present) | Tools & Skills section loads successfully |
| 8 | Verify Tools list displays for both versions (read-only) | Tools section visible; shows attached tools for each version |
| 9 | Verify Skills list displays for both versions (read-only) | Skills section visible; shows attached skills for each version |
| 10 | Return to Instructions section | Instructions section reloads with original content |
| 11 | Edit Instructions in Version 1 (left column) to "Updated base instructions" | Text updates in Version 1 column only |
| 12 | Verify Version 2 (right column) Instructions remains unchanged | Version 2 still shows original "V1 instructions" |
| 13 | Click Save button for Version 1 column | Save operation executes; success message or indicator appears |
| 14 | Close the Compare Versions modal | Modal closes |
| 15 | Reopen Compare Versions modal for same agent | Modal reopens with fresh data |
| 16 | Verify Version 1 Instructions shows saved changes: "Updated base instructions" | Version 1 displays the updated text |
| 17 | Verify Version 2 Instructions remains unchanged: "V1 instructions" | Version 2 was not affected by Version 1 save |
| 18 | Edit Instructions in Version 2 to "Updated v1.0 instructions" | Text updates in Version 2 column only |
| 19 | Click Save button for Version 2 column | Save operation executes; success message appears |
| 20 | Close and reopen modal | Modal reopens |
| 21 | Verify Version 2 now shows "Updated v1.0 instructions" | Version 2 displays saved changes |
| 22 | Verify Version 1 still shows "Updated base instructions" (unchanged by Version 2 save) | Version 1 unaffected by Version 2 save |
| 23 | Navigate to User Interaction section and edit Welcome Message in Version 1 | Welcome Message field updates |
| 24 | Save Version 1, close modal, reopen | Changes persist in Version 1 only |
| 25 | Verify Version 2 Welcome Message remains unchanged | Version 2 Welcome Message unaffected |

## Expected Final State

All three agent sections (Instructions, User Interaction, Tools & Skills) display correctly with content from both versions. Saving changes to one version does not affect the other version. Changes persist after modal close/reopen.

## Pass/Fail Criteria

**Pass:**
- All three sections are accessible and display correctly
- Instructions and User Interaction sections show editable fields
- Tools & Skills section displays read-only dependency lists
- Content from both versions visible side-by-side
- Saving Version 1 does not modify Version 2
- Saving Version 2 does not modify Version 1
- Saved changes persist after closing and reopening modal
- Independent save works for Instructions and Welcome Message fields

**Fail:**
- Any section is missing or fails to load
- Content from only one version is visible
- Saving one version affects the other version
- Changes do not persist after modal close/reopen
- Save button saves both versions instead of only the clicked version
- Editable fields are not functional or read-only when they should be editable
