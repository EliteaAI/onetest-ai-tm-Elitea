---
id: ELITEA-5020
title: "Verify Applications page: tabs, hidden Types filter, no folders, Discover cards and direct Add"
priority: critical
type: functional
module: new-sidebar
status: draft
execution_type: manual
tags: [r-2.0.9, eng:design, nfr:ui]
requirements: [EliteaAI/elitea_issues#7560, EliteaAI/elitea_issues#7571]
---
# ELITEA-5020: Verify Applications page: tabs, hidden Types filter, no folders, Discover cards and direct Add

## Preconditions

- User is logged in to `{{base_url}}`
- A private project and a team project with applications of both types

## Test Data

| Field | Value |
|-------|-------|
| Private project tabs | Yours / Discover |
| Team project tabs | Team / Discover |
| Types filter | Inventory, Wikis |
| Discover cards (order) | Wikis, Inventory |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open **Applications** from Explore in the private project, then in the team project | Tabs as in the Test Data; the project tab is selected by default |
| 2 | On the project tab, look at the page without clicking anything | Card view by default with a Table option; search **Search applications**; the **Types** filter is not visible |
| 3 | Click the filter icon | A panel opens on the right with **Types**: Inventory and Wikis — no Folders |
| 4 | Select one type, then click the filter icon again | The list shows only that type; the panel hides and the filter stays applied |
| 5 | Look for folder controls on every tab | No folders, folder creation or folder actions anywhere |
| 6 | Open **Discover** | **Wikis** then **Inventory** cards, each with **Configure** and **Documentation**; no view switch and no Types filter |
| 7 | Search in Discover, then use **Configure** and **Documentation** on a card | Search filters the cards; both actions open their existing destinations |
| 8 | Click **+ Add** | A direct button with no dropdown; it opens the existing application creation flow in the selected project |

## Expected Final State

All dialogs are closed and nothing was created.

## Pass/Fail Criteria

**Pass:**
- Tabs follow the project type; Types is hidden until the filter icon is clicked
- No folder controls anywhere; Discover cards and their actions work; **+ Add** is direct

**Fail:**
- Types is visible on page load or doesn't toggle
- Folder controls appear, or Discover shows the project view switch or filter
- **+ Add** shows a dropdown, Import or Build with AI
