---
id: ELITEA-4875
title: "Multi-email invite notifies only successfully added users"
priority: high
type: functional
module: notifications
status: draft
execution_type: manual
tags: [feat:admin-platform, feat:notifications, issue:7340, r-2.0.9]
requirements: ["EliteaAI/elitea_issues#7340"]
---

# ELITEA-4875: Multi-email invite notifies only successfully added users

**Module:** notifications · **Priority:** high · **Type:** functional

**Objective:** Verify each user added by one invite gets exactly one notification, while failed emails and the inviting admin get none.

---

## Preconditions

- User is logged in to `{{base_url}}`.
- Add toggle is on.
- User A is an admin of team project `mariam_test`; User B is logged in to `{{base_url}}` in a second browser profile.
- User D is already a member of `mariam_test`.

---

## Test Data

| Field | Value |
|-------|-------|
| User B | not a member |
| User C | not a member |
| User D | already a member |
| `invalid-email@` | invalid |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As User A open Invite users, enter all four emails comma-separated, role editor | Dialog accepts the input. |
| 2 | Submit | B and C are added; D shows "already exists"; the invalid email fails validation. |
| 3 | As User B and User C open the popover | Each has exactly one added notification. |
| 4 | As User D open the popover | No new notification. |
| 5 | As User A open the popover | No added notification. |

---

## Expected Final State

Only B and C were notified.

---

## Pass/Fail Criteria

**Pass:**
- Exactly 2 notifications
- None for D, the invalid email or the admin

**Fail:**
- Failed emails or the admin are notified
- B or C get none or a duplicate
