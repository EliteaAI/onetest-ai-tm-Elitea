---
id: ELITEA-4870
title: "Remove toggle on and off controls removal notifications without restart"
priority: critical
type: functional
module: admin-portal
status: draft
execution_type: manual
tags: [feat:admin-platform, feat:notifications, issue:7340, r-2.0.9]
requirements: ["EliteaAI/elitea_issues#7340"]
---

# ELITEA-4870: Remove toggle on and off controls removal notifications without restart

**Module:** admin-portal · **Priority:** critical · **Type:** functional

**Objective:** Verify saving the remove toggle on enables removal notifications and saving it off stops them immediately.

---

## Preconditions

- User is logged in to `{{base_url}}`.
- Logged in to `{{base_url}}` as a platform admin with access to the Admin portal.
- User A is an admin of team project `mariam_test`; User B is logged in to `{{base_url}}` in a second browser profile.
- User B is a member of `mariam_test`.

---

## Test Data

| Field | Value |
|-------|-------|
| Toggle | Notify users when removed from a team project |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Turn the remove toggle **on** and click **Save**; do not restart any service | Setting saved. |
| 2 | As User A remove User B from `mariam_test` | Removal succeeds. |
| 3 | As User B check the popover | Removal notification is present. |
| 4 | Invite User B again | Invite succeeds. |
| 5 | Turn the remove toggle **off** and click **Save** | Setting saved. |
| 6 | Remove User B again | Removal succeeds. |
| 7 | As User B check the popover and `GET` notifications API | No new removal notification was created. |

---

## Expected Final State

Remove toggle is off; User B has exactly one removal notification, from step 2.

---

## Pass/Fail Criteria

**Pass:**
- Notification only while the toggle is on
- No restart required

**Fail:**
- No notification while on
- New notification while off
- Restart required
