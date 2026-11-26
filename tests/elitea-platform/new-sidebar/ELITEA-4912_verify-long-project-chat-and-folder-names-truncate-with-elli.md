---
id: ELITEA-4912
title: "Verify long project, chat and folder names truncate with ellipsis"
priority: medium
type: functional
module: new-sidebar
status: draft
execution_type: manual
tags: [r-2.0.9, eng:design, nfr:ui]
requirements: [EliteaAI/elitea_issues#7562]
---
# ELITEA-4912: Verify long project, chat and folder names truncate with ellipsis


## Preconditions

- User is logged in to `{{base_url}}`
- The test data items below exist

## Test Data

| # | Item | Value |
|---|------|-------|
| 1 | Project name | `Very long project name for sidebar truncation testing 0123456789` |
| 2 | Chat name | `Extremely long chat name used to verify ellipsis behaviour in the sidebar history list 0123456789` |
| 3 | Folder name | `Long folder name checking truncation inside the chats area 0123456789` |
| 4 | Pinned chat with long name | Same as row 2, pinned |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open `{{base_url}}/app/` with the sidebar expanded and select the long-named project | The project name is truncated with an ellipsis inside the selector, and the sidebar stays 288 px wide |
| 2 | Look at the long-named chat and folder in the Chats history | The names end with an ellipsis, and the row icons and actions (pin, menu) stay visible and aligned |
| 3 | Hover a truncated name | The full name is shown in a tooltip (if supported on dev) |
| 4 | Collapse and expand the sidebar | Truncation stays correct, and no horizontal scrollbar appears in the sidebar |

## Expected Final State

Long names never widen or break the sidebar.

## Pass/Fail Criteria

**Pass:**
- Every long name is truncated with an ellipsis, and the width and row actions are unaffected

**Fail:**
- Text wraps or overflows, the sidebar widens, a horizontal scrollbar appears, or row actions are pushed out
