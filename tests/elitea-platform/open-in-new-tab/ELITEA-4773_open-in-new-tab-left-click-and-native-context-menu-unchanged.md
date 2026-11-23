---
id: ELITEA-4773
title: "Open in new tab: Plain left-click and native context menu unchanged"
priority: critical
type: functional
module: open-in-new-tab
status: ready
execution_type: manual
tags: [open-in-new-tab, regression, left-click, context-menu, release:2.0.9, issue:7478]
requirements: [EliteaAI/elitea_issues#7478]
---
# ELITEA-4773: Open in new tab: Plain left-click and native context menu unchanged

**Module:** open-in-new-tab · **Priority:** Critical · **Type:** Functional

**Objective:** Regression check that plain left-click still navigates in the same tab as before and that right-click shows only the browser's native menu.

**Coverage:**
- Left-click on sidebar item, card, table name, Run History, Evaluate
- Browser Back navigation
- Native context menu not replaced or blocked

## Preconditions
- User is logged in; at least one Agent and one Pipeline exist.

## Test Data
- Agent `QA-Agent-NewTab`, Pipeline `QA-Pipeline-NewTab`

## Steps
| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Left-click a **sidebar item** (e.g., Agents) | Page opens in the same tab; no new tab |
| 2 | Left-click an **agent card** | Agent configuration opens in the same tab |
| 3 | Press browser **Back** | Returns to the Agents list with previous state (view, filters) |
| 4 | Switch to table view and left-click an **agent name** | Agent opens in the same tab |
| 5 | Open the three-dot menu and left-click **Run History** | Run History opens in the same tab |
| 6 | Open the pipeline three-dot menu and left-click **Evaluate (Beta)** | Evaluate page opens in the same tab |
| 7 | Right-click a sidebar item, a card, a table name, and a menu link | Only the browser's native context menu appears; no custom ELITEA menu replaces or blocks it |

## Expected Final State
Left-click behaviour is identical to before the change; native context menu works everywhere.

## Pass/Fail Criteria
- **Pass:** All left-clicks navigate in the same tab, Back works, and only native menus appear on right-click.
- **Fail:** A left-click opens a new tab, does nothing, or a custom menu appears/blocks the native one.
