---
id: ELITEA-4225
title: "Verify long toolkit page stays usable with both sections expanded"
priority: medium
type: functional
module: toolkits-indexes
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.8]
requirements: [EliteaAI/elitea_issues#7045]
---
# ELITEA-4225: Verify long toolkit page stays usable with both sections expanded

## Preconditions

- User is logged in to `{{base_url}}`
- Private project is selected
- Toolkits exist: `Jira_Management` (23 tools) and GitHub (many tools)
- Configuration and TOOLS sections are expanded

## Test Data

| Field | Value |
|-------|-------|
| Window size | 1366 × 768 |
| Toolkits | `Jira_Management`, GitHub |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Set the browser window to 1366 × 768 and open `Jira_Management`. | The details page opens with both sections expanded. |
| 2 | Scroll the left panel. | The left panel scrolls on its own; the Indexes panel stays in place. |
| 3 | While scrolled down, look at the header. | The Save, Discard, Test and Run History buttons stay visible and clickable. |
| 4 | Scroll to the end of the TOOLS list. | The last tool card is fully visible and not hidden behind other elements. |
| 5 | Repeat steps 1–4 for the GitHub toolkit. | Same results as for `Jira_Management`. |

## Expected Final State

The toolkit details page stays usable at 1366 × 768 with both sections expanded.

## Pass/Fail Criteria

**Pass:**
- The left panel scrolls independently and the header stays usable
- All tool cards are reachable and fully visible

**Fail:**
- The page or panels can't be scrolled to the end
- Header buttons are hidden or not clickable
- Tool cards are cut off or overlapped
