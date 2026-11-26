---
id: ELITEA-4909
title: "Verify collapsing and expanding the sidebar keeps the current page and unsaved work"
priority: high
type: functional
module: new-sidebar
status: ready
execution_type: manual
tags: [r-2.0.9, eng:design, nfr:ui]
requirements: [EliteaAI/elitea_issues#7562]
---
# ELITEA-4909: Verify collapsing and expanding the sidebar keeps the current page and unsaved work


## Preconditions

- User is logged in to `{{base_url}}`

## Test Data

| # | Page | Unsaved work |
|---|------|--------------|
| 1 | Chat | Text typed in the message input, not sent |
| 2 | Agent configuration | Edited instructions, not saved |
| 3 | Chat history | Scrolled down, one folder expanded |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the page and create the unsaved state from the Test Data row | The unsaved state is visible |
| 2 | Click the existing collapse control | The sidebar collapses to the compact rail, and the page doesn't change or reload |
| 3 | Click the expand control | The sidebar expands |
| 4 | Check the page | The same page is open and the unsaved work is intact (row 3: scroll position and folder expansion kept) |

## Expected Final State

The sidebar toggles without side effects on the page.

## Pass/Fail Criteria

**Pass:**
- No navigation, reload or loss of unsaved input for any row

**Fail:**
- The URL changes, the page reloads, or the typed or edited content is lost
