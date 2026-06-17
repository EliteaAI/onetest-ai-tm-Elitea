---
id: ELITEA-0748
title: "Notifications Popup — Infinite scroll appends new groups, last partial group displayed correctly"
priority: critical
type: functional
module: notifications
status: ready
execution_type: manual
tags: [feat:notifications, eng:frontend, r-2.0.2]
requirements: [EliteaAI/elitea_issues#4724, EliteaAI/elitea_issues#4726, EliteaAI/elitea_issues#4753]
---
# ELITEA-0748: Notifications Popup — Infinite scroll appends new groups, last partial group displayed correctly

**Module:** Notifications · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that scrolling through the notifications popup appends each new group below the previously loaded ones (infinite scroll), all groups remain visible simultaneously, and the last group is always displayed — even when it contains fewer than 20 items.

**Coverage:**
- Previously loaded notification groups are NOT replaced when scrolling to load the next group (EliteaAI/elitea_issues#4726)
- Notifications from all loaded groups are visible at the same time
- Last group (< 20 items) is displayed correctly and does not auto-trigger another load (EliteaAI/elitea_issues#4724)
- "No notifications right now" empty state does NOT appear while real notifications exist

## Preconditions

- Logged in to the platform
- More than 20 notifications exist (at least 3 groups worth, with the last group containing fewer than 20 items)
- Notifications popup is accessible via the bell icon in the sidebar

## Test Data

- Requires 20+ notifications, with the final group containing fewer than 20 items
- Note visible notification titles from group 1 before scrolling, to verify they persist after loading group 2

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Click the bell icon to open the notifications popup. | Popup opens. The first group of notifications (up to 20) is displayed. |
| 2 | Note the titles/content of the currently visible notifications. | Notifications from the first group are recorded for comparison. |
| 3 | Scroll to the bottom of the popup to trigger loading of the next group. | New notifications load and are appended below the existing ones. The previously visible notifications from group 1 remain visible above. |
| 4 | Continue scrolling to load additional groups until the last group is reached (visible by it containing fewer than 20 items). | Each new group is appended below all previous groups. At no point do earlier notifications disappear. |
| 5 | Observe the popup after the last group has loaded. | The last group (< 20 items) is displayed correctly. No additional load is triggered automatically. The 'No notifications right now' empty state does NOT appear. |
| 6 | Verify all previously loaded groups are still visible by scrolling up and down. | All notifications from all groups are accessible within the same popup session. |

## Expected Final State

All notifications from all groups are accessible within the same popup session.

## Pass/Fail Criteria

**Pass:**
- Each scroll-load appends new notifications below existing ones — prior groups remain visible
- All notifications from all loaded groups are simultaneously visible
- Last group (< 20 items) is shown correctly without triggering an extra empty load
- "No notifications right now" does not appear while real notifications are present

**Fail:**
- Previously loaded group disappears when the next group loads (replaced instead of appended)
- Last group is replaced by "No notifications right now" empty state
- Any real notifications are hidden due to incorrect pagination behavior
