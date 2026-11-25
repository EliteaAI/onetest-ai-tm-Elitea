---
id: ELITEA-4868
title: "Removed user receives plain-text removal notification when remove toggle is on"
priority: critical
type: functional
module: notifications
status: draft
execution_type: manual
tags: [feat:admin-platform, feat:notifications, issue:7340, r-2.0.9]
requirements: ["EliteaAI/elitea_issues#7340"]
---

# ELITEA-4868: Removed user receives plain-text removal notification when remove toggle is on

**Module:** notifications · **Priority:** critical · **Type:** functional

**Objective:** Verify a user removed from a team project receives one removal notification with no link.

---

## Preconditions

- User is logged in to `{{base_url}}`.
- Remove toggle is on and saved.
- User A is an admin of team project `mariam_test`; User B is logged in to `{{base_url}}` in a second browser profile.
- User B is a member of `mariam_test`.

---

## Test Data

| Field | Value |
|-------|-------|
| Project | `mariam_test` |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As User A open `mariam_test` → Settings → Users | Users list loads; User B is listed. |
| 2 | Click the delete icon on User B's row and confirm | User B is removed from the list. |
| 3 | As User B open the bell popover | Unread dot is shown. |
| 4 | Check the newest notification | Exactly one notification: "You have been removed from mariam_test project." |
| 5 | Hover and click every part of the text, including `mariam_test` | Nothing is a link; no navigation happens. |
| 6 | Check the icon | A "person removed" icon, different from the added icon. |

---

## Expected Final State

User B has one plain-text removal notification.

---

## Pass/Fail Criteria

**Pass:**
- One notification with correct text
- No link, removal icon shown

**Fail:**
- No notification or a duplicate
- Project name is clickable
- Wrong text
