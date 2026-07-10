---
id: ELITEA-1801
title: "Expand widget to full-view mode and collapse back"
priority: medium
type: functional
module: support-assistant
status: draft
execution_type: automated
automation_test_id: tests.ui.support_assistant.test_support_assistant_smoke.TestSupportAssistantViewModes.test_expand_and_collapse_to_full_view
tags: [automated:UI:regression, feat:support-assistant]
requirements: []
---

# ELITEA-1801: Expand widget to full-view mode and collapse back

**Module:** support-assistant · **Priority:** medium · **Type:** functional

**Objective:** Verify that the Support Assistant widget starts in compact mode (default), can be expanded to full-view mode via the Expand button, and can be collapsed back to widget mode; the widget remains open and functional in both states.

---

## Preconditions

- User is authenticated (browser context pre-loaded with `auth_state` via `page` fixture).
- Support Assistant feature is enabled.
- Widget is in compact (default) mode when opened.

---

## Test Data

| Field | Value |
|-------|-------|
| Expand button selector | `button[data-testid="support-assistant-expand"]` |
| Expand button fallback | `button[aria-label="Expand chat"]` |
| Animation wait | 500 ms |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the Chat page (`/chat`) | Page loads successfully |
| 2 | Open the Support Assistant widget | Widget panel opens in compact mode; title is visible |
| 3 | Wait for the widget to be fully ready | Widget title and message input are visible |
| 4 | Click the Expand button (`data-testid="support-assistant-expand"`) | Expand action is triggered; 0.5 s animation wait completes |
| 5 | Wait 500 ms for the expand animation to complete | Animation finishes |
| 6 | Assert that the widget is still open in full-view mode | `is_widget_open()` returns `True`; widget title is still visible |
| 7 | Click the Expand/Collapse toggle button again to collapse back to widget mode | Same button (`data-testid="support-assistant-expand"`) acts as a toggle; 0.5 s animation wait completes |
| 8 | Wait 500 ms for the collapse animation | Animation finishes |
| 9 | Assert that the widget is still open in compact widget mode | `is_widget_open()` returns `True`; widget title is still visible |

---

## Expected Final State

The Support Assistant widget expands to full-view mode when the Expand button is clicked and collapses back to compact widget mode when the toggle is clicked again. The widget remains open and the title is visible in both states.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Widget is open and title is visible after expanding to full-view.
- Widget is open and title is visible after collapsing back to compact mode.

**Fail:**
- Any step produces an error or unexpected result.
- Widget closes during expand or collapse.
- Expand/collapse toggle does not change the view mode.
