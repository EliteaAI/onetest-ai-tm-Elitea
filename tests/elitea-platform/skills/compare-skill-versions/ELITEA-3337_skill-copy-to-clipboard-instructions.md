---
id: ELITEA-3337
title: "Copy to clipboard works for Skill Instructions fields in version comparison"
priority: high
type: functional
module: skills
status: draft
execution_type: manual
tags: [feat:skills, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6304]
---

## Preconditions

- User is logged in to `{{base_url}}` with edit permissions
- Skill exists with 2+ versions containing Instructions
- External text editor available for paste verification

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/skills` |
| Test Instructions V1 | "This skill performs data analysis using advanced algorithms and machine learning techniques." |
| Test Instructions V2 | "This skill performs comprehensive data analysis with visualization capabilities." |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open Compare Versions modal for Test Skill | Modal opens successfully |
| 2 | Locate copy-to-clipboard button/icon for Instructions field in Version 1 column | Copy button/icon is visible near Instructions field |
| 3 | Click the copy button for Version 1 Instructions | Success feedback appears (toast notification or checkmark icon) |
| 4 | Open external text editor and paste (Ctrl+V or Cmd+V) | Instructions text is pasted correctly: "This skill performs data analysis using advanced algorithms and machine learning techniques." |
| 5 | Return to Compare Versions modal | Modal still open |
| 6 | Locate copy button for Version 2 Instructions field | Copy button is visible |
| 7 | Click copy button for Version 2 Instructions | Success feedback appears |
| 8 | Paste into external editor | Version 2 Instructions text pastes correctly: "This skill performs comprehensive data analysis with visualization capabilities." |
| 9 | Verify correct content was copied for each version | Each copy operation captured the correct version's Instructions |

## Expected Final State

Copy to clipboard functionality works for Instructions field in both version columns with success feedback and correct content pasted.

## Pass/Fail Criteria

**Pass:**
- Copy button visible and functional for Instructions field in both columns
- Success feedback displayed after copy action
- Correct content pasted into external editor for each version
- Copy works independently for both version columns

**Fail:**
- Copy button missing or non-functional
- No success feedback after copy
- Incorrect content pasted
- Copy only works for one column
