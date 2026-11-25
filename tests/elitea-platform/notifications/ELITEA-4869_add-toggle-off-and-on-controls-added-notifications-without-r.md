---
id: ELITEA-4869
title: "Add toggle off and on controls added notifications without restart"
priority: critical
type: functional
module: admin-portal
status: draft
execution_type: manual
tags: [feat:admin-platform, feat:notifications, issue:7340, r-2.0.9]
requirements: ["EliteaAI/elitea_issues#7340"]
---

# ELITEA-4869: Add toggle off and on controls added notifications without restart

**Module:** admin-portal · **Priority:** critical · **Type:** functional

**Objective:** Verify saving the add toggle off suppresses added notifications and saving it on restores them immediately.

---

## Preconditions

- User is logged in to `{{base_url}}`.
- Logged in to `{{base_url}}` as a platform admin with access to the Admin portal.
- User A is an admin of team project `mariam_test`; User B is logged in to `{{base_url}}` in a second browser profile.
- User B is not a member of `mariam_test`.

---

## Test Data

| Field | Value |
|-------|-------|
| Toggle | Notify users when added to a team project |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | In Admin → Features → Notifications turn the add toggle **off** and click **Save** | Setting saved. |
| 2 | As User A invite User B to `mariam_test` | Invite succeeds. |
| 3 | As User B check the popover and `GET` notifications API | No added notification exists. |
| 4 | As User A remove User B | Removal succeeds. |
| 5 | Turn the add toggle **on** and click **Save**; do not restart any service | Setting saved. |
| 6 | Invite User B again | Invite succeeds. |
| 7 | As User B check the popover | Added notification is present. |

---

## Expected Final State

Add toggle is on; User B has exactly one added notification, from the second invite.

---

## Pass/Fail Criteria

**Pass:**
- No notification while off
- Notification once back on, without restart

**Fail:**
- Notification created while off
- None after turning on
- Restart required
