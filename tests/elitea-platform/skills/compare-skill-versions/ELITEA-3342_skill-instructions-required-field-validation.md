---
id: ELITEA-3342
title: "Skill Instructions cannot be deleted - required field validation enforced in comparison modal"
priority: high
type: functional
module: skills
status: draft
execution_type: manual
tags: [feat:skills, r-2.0.6, bug:6565]
requirements: [EliteaAI/elitea_issues#7675, EliteaAI/elitea_issues#6304, EliteaAI/elitea_issues#6565]
---

## Preconditions

- User is logged in to `{{base_url}}` with edit permissions
- Skill exists with 2+ versions containing Instructions

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/skills` |
| Version 1 Instructions | "This skill performs data analysis and reporting tasks." |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open Compare Versions modal for Test Skill | Modal opens successfully |
| 2 | Verify Instructions field in Version 1 contains text: "This skill performs data analysis and reporting tasks." | Instructions field is populated |
| 3 | Select all text in Version 1 Instructions field | Text is selected |
| 4 | Delete all content from Instructions field (Backspace or Delete key) | Field is now empty |
| 5 | Hover the **Save** button in the Version 1 header | Save is disabled |
| 6 | Verify the tooltip on the disabled Save | Tooltip is displayed |
| 7 | Verify the tooltip indicates Instructions is required | Tooltip: "Instructions cannot be empty." |
| 8 | Verify the Save cannot be clicked (no success message) | Save does not execute |
| 9 | Verify Instructions field remains empty after failed save attempt | Field is still empty (unsaved state) |
| 10 | Close and reopen Compare Versions modal | Modal opens with fresh data |
| 11 | Verify Version 1 Instructions shows original text (empty value was NOT saved) | Original text is displayed: "This skill performs data analysis and reporting tasks." |
| 12 | Repeat Steps 3-7 for Version 2 Instructions | Version 2 header Save is disabled with the same tooltip |

## Expected Final State

Skill Instructions field enforces required field validation during comparison. Empty Instructions cannot be saved, validation error message is displayed, and save operation is prevented.

## Pass/Fail Criteria

**Pass:**
- Attempting to save empty Instructions triggers validation error
- Clear error message indicates Instructions is required
- Save operation is prevented when Instructions is empty
- Empty Instructions are NOT persisted (original value retained)
- Validation works for both version columns

**Fail:**
- Empty Instructions can be saved without error
- No validation error message displayed
- Save succeeds with empty Instructions
- Empty value is persisted
