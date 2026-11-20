---
id: ELITEA-4772
title: "Open in new tab: Ctrl/Cmd+Click and middle-click open a new tab"
priority: high
type: functional
module: open-in-new-tab
status: ready
execution_type: manual
tags: [open-in-new-tab, modifier-click, middle-click, release:2.0.9, issue:7478]
requirements: [EliteaAI/elitea_issues#7478]
---
# ELITEA-4772: Open in new tab: Ctrl/Cmd+Click and middle-click open a new tab

**Module:** open-in-new-tab · **Priority:** High · **Type:** Functional

**Objective:** Verify that Ctrl+Click (Windows) / Cmd+Click (macOS) and middle-click on navigation links open the destination in a new tab while the current tab stays in place.

**Coverage:**
- Link types: sidebar item, entity card, table entity name, three-dot menu link
- Click types: Ctrl/Cmd+Click, middle-click

## Preconditions
- User is logged in; at least one Agent exists.
- Use Ctrl+Click on Windows or Cmd+Click on macOS.

## Test Data
- Agent `QA-Agent-NewTab`

## Steps
| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Ctrl/Cmd+Click a **sidebar item** (e.g., Pipelines) | Pipelines opens in a background tab; current tab stays on its page |
| 2 | Ctrl/Cmd+Click an **agent card** (card view) | Agent opens in a background tab; current tab stays on the list |
| 3 | Ctrl/Cmd+Click an **agent name** (table view) | Agent opens in a background tab; current tab stays on the list |
| 4 | Open the agent's three-dot menu and Ctrl/Cmd+Click **Run History** | Run History opens in a background tab; current tab stays |
| 5 | Middle-click a **sidebar item** | Destination opens in a new tab; current tab stays |
| 6 | Middle-click an **agent card** | Agent opens in a new tab; current tab stays |
| 7 | Middle-click an **agent name** in table view | Agent opens in a new tab; current tab stays |
| 8 | Middle-click **Run History** in the three-dot menu | Run History opens in a new tab; current tab stays |

## Expected Final State
Modifier-click and middle-click open new tabs with correct destinations; the original tab is never navigated.

## Pass/Fail Criteria
- **Pass:** All 8 clicks open the correct page in a new tab and the current tab does not change.
- **Fail:** Any click navigates the current tab, opens nothing, or opens a wrong page.
