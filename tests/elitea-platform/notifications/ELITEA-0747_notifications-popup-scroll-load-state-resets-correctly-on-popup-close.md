---
id: ELITEA-0747
title: "Notifications Popup — Scroll load state resets correctly on popup close and reopen"
priority: critical
type: functional
module: notifications
status: ready
execution_type: manual
tags: [feat:notifications, eng:frontend, r-2.0.2]
requirements: [EliteaAI/elitea_issues#4725]
---
# ELITEA-0747: Notifications Popup — Scroll load state resets correctly on popup close and reopen

**Module:** Notifications · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that closing and reopening the notifications popup fully resets the scroll load state — starting from the first group and correctly loading subsequent groups on scroll.

**Coverage:**
- Scroll load state is cleared when the popup is closed (#4725)
- On reopen, the first group of notifications is shown (not a stale mid-session state)
- Scrolling after reopen loads subsequent groups correctly
- Behavior is consistent across multiple close/reopen cycles

## Preconditions

- Logged in to the platform
- More than 20 notifications exist (enough for at least 2 groups)
- Notifications popup is accessible via the bell icon

## Test Data

- Requires 20+ notifications to have at least 2 full groups available for loading

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Click the bell icon to open the notifications popup. | Popup opens showing the first group of notifications. |
| 2 | Scroll to the bottom to trigger loading of the next group. | Second group of notifications loads and appends below the first. |
| 3 | Close the popup by clicking outside it or clicking the bell icon again. | Popup closes. |
| 4 | Reopen the popup by clicking the bell icon. | Popup opens fresh, showing only the first group of notifications (most recent). No stale state from the previous session is present. |
| 5 | Scroll to the bottom of the popup. | The next group of notifications loads and appends correctly — same behavior as the very first open. |
| 6 | Close and reopen the popup a second time. Repeat steps 4–5. | Scroll load state resets again. Behavior is consistent across multiple open/close cycles. |

## Expected Final State

Scroll load state resets again. Behavior is consistent across multiple open/close cycles.

## Pass/Fail Criteria

**Pass:**
- After reopen, popup shows the first group of notifications (most recent)
- Scrolling correctly loads and appends the next group
- Behavior is identical to the very first open of the session

**Fail:**
- After reopen, only a single group is shown and scrolling loads nothing more
- Scrolling triggers no additional loading (scroll load appears stuck/disabled)
- A full page reload is required to restore correct scroll loading behavior
