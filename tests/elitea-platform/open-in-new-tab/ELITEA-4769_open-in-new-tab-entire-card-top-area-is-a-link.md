---
id: ELITEA-4769
title: "Open in new tab: Entire card top area is a link"
priority: medium
type: functional
module: open-in-new-tab
status: ready
execution_type: manual
tags: [open-in-new-tab, card-view, ui, release:2.0.9, issue:7478]
requirements: [EliteaAI/elitea_issues#7478]
---
# ELITEA-4769: Open in new tab: Entire card top area is a link

**Module:** open-in-new-tab · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that the link area covers the whole card top area (icon, title, empty space), not only the title text.

**Coverage:**
- Card icon, title, empty space in the card header
- At least two entity types

## Preconditions
- User is logged in.
- At least one Agent and one Pipeline exist; card view is selected.

## Test Data
- Any Agent card and any Pipeline card

## Steps
| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | On the Agents list, right-click the **icon** of an agent card | Native link menu with "Open link in new tab" appears |
| 2 | Right-click the **title** of the same card | Native link menu with "Open link in new tab" appears |
| 3 | Right-click **empty space** in the top area of the card (next to/below the title) | Native link menu with "Open link in new tab" appears |
| 4 | Select "Open link in new tab" from the menu opened in step 3 | New tab opens the same agent |
| 5 | Repeat steps 1–3 on a **Pipeline** card | Same link menu appears in all three spots |

## Expected Final State
The whole card top area behaves as one link on every tested card type.

## Pass/Fail Criteria
- **Pass:** The link menu appears on icon, title, and empty top-area space for both card types.
- **Fail:** Any of these spots shows only the generic page menu (no "Open link in new tab").
