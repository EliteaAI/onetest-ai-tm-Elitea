---
id: ELITEA-0194
title: "TC-020: Validation Summary Details Popup Shows Per-Issue Field, Issue, and Fix Breakdown With Copy Function"
priority: high
type: functional
module: agents-publishing
status: draft
execution_type: manual
tags: [feat:agents, story:3772, r-2.0.2]
requirements: [ProjectAlita/projectalita.github.io#3772]
---
# ELITEA-0194: TC-020: Validation Summary Details Popup Shows Per-Issue Field, Issue, and Fix Breakdown With Copy Function

**Module:** Agents Publishing · **Priority:** High · **Type:** Functional

**Objective:** Verify that the SUMMARY DETAILS section on the validation result screen includes an expand icon that opens a full popup with structured per-issue detail (Field, Issue, Fix) for critical issues and warnings, a copy icon to copy all details to clipboard, and that the popup can be closed independently without resetting the main modal.

Coverage:
- Expand icon on SUMMARY DETAILS opens a "Summary Details" popup
- Popup shows all three sections: Critical issues – N, Warnings – N, Suggestions – N
- Each critical/warning item shows: issue title, "Field: [name]", "Issue: [description]", "Fix: [action]"
- Copy icon copies all details to clipboard
- Popup can be closed independently; main Validation step modal remains open and unaffected

## Preconditions

- Logged in as User A
- Use Agent D (triggers critical issues — red banner) OR Agent E (triggers warnings — orange banner)
- Validation has run and results are displayed

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | After validation completes with at least one Critical or Warning issue, locate 'SUMMARY DETAILS' | SUMMARY DETAILS section is visible below the SUMMARY counts |
| 2 | Click the expand / fullscreen icon on the SUMMARY DETAILS section | A 'Summary Details' popup opens (fullscreen overlay or large modal) |
| 3 | Read the section headers in the popup | Popup contains sections: 'Critical issues – N', 'Warnings – N', 'Suggestions – N' |
| 4 | Read a Critical issue entry (e.g., 'Agent Description is missing') | Entry shows: issue title + 'Field: Description' + 'Issue: Description field is empty' + 'Fix: Add a clear description of what your agent does' |
| 5 | Read a Warnings entry (e.g., sub-agent description warning) | Entry shows the warning title with brief description |
| 6 | Read a Suggestions entry | Entry shows suggestion (e.g., 'Consider using semantic versioning (v1.0.0)') |
| 7 | Click the copy icon in the popup | All summary details are copied to clipboard; a visual confirmation appears (tooltip or icon change) |
| 8 | Click the close button (X or similar) on the popup | Popup closes; main validation result view is still displayed with banner, SUMMARY, and Publish button state unchanged |

## Expected Final State

Popup closes; main validation result view is still displayed with banner, SUMMARY, and Publish button state unchanged

## Pass/Fail Criteria

PASS:
- Expand icon opens the Summary Details popup
- Popup contains all three sections (Critical, Warnings, Suggestions) with correct counts
- Each critical issue entry provides structured Field / Issue / Fix detail (not just a title)
- Copy icon copies content to clipboard with visual confirmation
- Closing the popup returns to the main validation result view with all state preserved

FAIL:
- Expand icon does not open any popup
- Popup is missing one or more sections
- Issue entries show title only, without Field / Issue / Fix structured detail
- Copy function is absent or copies nothing
- Closing the popup also resets or closes the main publish modal
