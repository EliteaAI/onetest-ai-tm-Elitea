---
id: ELITEA-4223
title: "Verify start screen tools grid switches from two columns to one on narrow viewports"
priority: medium
type: functional
module: toolkits-indexes
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.8]
requirements: [EliteaAI/elitea_issues#7045]
---
# ELITEA-4223: Verify start screen tools grid switches from two columns to one on narrow viewports

## Preconditions

- User is logged in to `{{base_url}}`
- Private project is selected
- Toolkits exist: `Jira_Management` (Jira) and GitHub

## Test Data

| Window width | Expected grid |
|--------------|---------------|
| 1920px | Two columns |
| ~1280px | Two columns |
| ~1024px | Two columns |
| ~590px | One column |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open `Jira_Management` → **Test** in a 1920px-wide window. | Tools are shown in a two-column grid with no overlap or cut-off text. |
| 2 | Resize the window to about 1280px, then 1024px. | The grid stays two columns and the buttons stay readable. |
| 3 | Resize the window to about 590px. | The grid switches to one column. |
| 4 | Open the GitHub toolkit → **Test** and look at long tool names at each width. | Long names wrap or truncate cleanly; buttons in one row keep the same height. |
| 5 | At 1280px, collapse and expand the left sidebar. | The grid adapts to the new width without overlap. |

## Expected Final State

The start-screen grid shows two columns on wide windows and one column on narrow windows, with no layout breaks.

## Pass/Fail Criteria

**Pass:**
- Two columns on wide windows, one column at about 590px
- No overlapping or cut-off buttons at any width

**Fail:**
- The grid stays two columns on a narrow window
- Buttons overlap, are cut off, or have uneven height in a row
