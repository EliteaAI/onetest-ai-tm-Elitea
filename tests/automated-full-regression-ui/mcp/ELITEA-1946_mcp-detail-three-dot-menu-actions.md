---
id: ELITEA-1946
title: "MCP Detail — Three-Dot Menu Actions"
priority: medium
type: functional
module: elitea-platform
status: ready
execution_type: automated
tags: [automated:UI:regression]
requirements: []
automation_test_id: tests.ui.toolkits.test_mcp_three_dot_menu_actions.test_mcp_detail_three_dot_menu_actions
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1736
---

# ELITEA-1946: MCP Detail — Three-Dot Menu Actions

**Module:** elitea-platform · **Priority:** medium · **Type:** functional

**Objective:** Verify that the three-dot context menu on a Remote MCP detail page displays the expected actions, and that "Copy link" and "Pin to top" actions function correctly.

---

## Preconditions

- User is logged in to the Elitea platform.
- A Remote MCP detail page is open.

---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open any Remote MCP detail page | Detail page loads |
| 2 | Click the three-dot menu button (top-right, next to Save/Discard) | Menu opens |
| 3 | Verify menu opens with options: Export (disabled), Fork (disabled), Copy link, Pin to top, Delete | All expected menu items are visible with correct states |
| 4 | Click "Copy link" — verify link is copied to clipboard (or toast confirmation with "The link has been copied to the clipboard") | Copy confirmation toast is shown |
| 5 | Close menu (click outside or press Escape) | Menu closes |
| 6 | Reopen menu and click "Pin to top" — verify MCP gets pinned | MCP is pinned |
| 7 | Navigate to list — verify MCP appears at top | MCP is at the top of the list |

---

## Expected Final State

The MCP is pinned and appears at the top of the MCP list after selecting "Pin to top" from the three-dot menu.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Menu shows correct options; Copy link and Pin to top work as expected.

**Fail:**
- Any step produces an error or unexpected result.
- Menu items are missing, Copy link fails, or Pin to top has no effect.
