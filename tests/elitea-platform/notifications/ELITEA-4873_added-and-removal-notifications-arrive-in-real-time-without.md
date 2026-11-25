---
id: ELITEA-4873
title: "Added and removal notifications arrive in real time without page reload"
priority: high
type: functional
module: notifications
status: draft
execution_type: manual
tags: [feat:admin-platform, feat:notifications, issue:7340, r-2.0.9]
requirements: ["EliteaAI/elitea_issues#7340"]
---

# ELITEA-4873: Added and removal notifications arrive in real time without page reload

**Module:** notifications · **Priority:** high · **Type:** functional

**Objective:** Verify both membership notifications are delivered live to an online user within 5 seconds.

---

## Preconditions

- User is logged in to `{{base_url}}`.
- Both toggles are on and saved.
- User A is an admin of team project `mariam_test`; User B is logged in to `{{base_url}}` in a second browser profile.
- User B has the bell popover open.

---

## Test Data

| Field | Value |
|-------|-------|
| Added max delay | 5 s |
| Removed max delay | 5 s |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As User A invite User B to `mariam_test`; start a timer | Invite succeeds. |
| 2 | Watch User B's open popover without reloading | Added notification and unread dot appear within 5 s. |
| 3 | As User A remove User B; start a timer | Removal succeeds. |
| 4 | Watch User B's popover without reloading | Removal notification and unread dot appear within 5 s. |

---

## Expected Final State

Both notifications were delivered live.

---

## Pass/Fail Criteria

**Pass:**
- Each notification appears within 5 s without reload

**Fail:**
- Reload needed
- Delay over 5 s
