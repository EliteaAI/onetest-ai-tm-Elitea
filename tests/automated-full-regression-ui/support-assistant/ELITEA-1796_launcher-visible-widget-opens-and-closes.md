---
id: ELITEA-1796
title: "Launcher is visible and Support Assistant widget opens and closes"
priority: high
type: functional
module: support-assistant
status: ready
execution_type: automated
automation_test_id: tests.ui.support_assistant.test_support_assistant_smoke.TestSupportAssistantLauncher.test_launcher_visible_and_opens_widget
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/289
tags: [automated:UI:regression, feat:support-assistant]
requirements: []
---

# ELITEA-1796: Launcher is visible and Support Assistant widget opens and closes

**Module:** support-assistant · **Priority:** high · **Type:** functional

**Objective:** Verify that the floating Support Assistant launcher button is visible on the Chat page, that clicking it opens the widget panel, and that clicking the Close (X) button dismisses the panel while the launcher remains visible.

---

## Preconditions

- User is authenticated (browser context pre-loaded with `auth_state` via `page` fixture).
- Support Assistant feature is enabled for the current deployment.

---

## Test Data

| Field | Value |
|-------|-------|
| Page to navigate to | `/chat` |
| Launcher selector | `button[data-testid="support-assistant-launcher"]` |
| Widget title selector | `data-testid="support-assistant-title"` |
| Close button selector | `button[data-testid="support-assistant-close"]` |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the Chat page (`/chat`) | Page loads and DOM content is ready |
| 2 | Assert that the Support Assistant launcher button is visible | `button[data-testid="support-assistant-launcher"]` (or fallback `button.elitea-assistant-button` / `button[aria-label="Support Assistant"]`) is visible on the page |
| 3 | Click the launcher button to open the widget | Widget panel opens; `data-testid="support-assistant-title"` (or `h2:has-text("ELITEA Support")`) becomes visible |
| 4 | Assert that the widget is open | Widget title element is visible; `is_widget_open()` returns `True` |
| 5 | Click the Close (X) button to dismiss the widget | `button[data-testid="support-assistant-close"]` (or `button[aria-label="Close chat"]`) is clicked; widget title becomes hidden |
| 6 | Assert that the widget is no longer open | `is_widget_open()` returns `False`; widget title is not visible |
| 7 | Assert that the launcher button is still visible | Launcher button remains visible after the widget is closed |

---

## Expected Final State

The Support Assistant launcher is visible on the Chat page. The widget panel opens after clicking the launcher and closes after clicking the X button. The launcher button remains visible after the widget is closed.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Launcher is visible before and after open/close cycle.
- Widget opens on launcher click and closes on X click.

**Fail:**
- Any step produces an error or unexpected result.
- Launcher is not visible, widget does not open, or widget does not close.
