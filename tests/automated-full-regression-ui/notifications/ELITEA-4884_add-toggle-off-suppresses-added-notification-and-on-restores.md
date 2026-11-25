---
id: ELITEA-4884
title: "Add toggle off suppresses added notification and on restores it"
priority: critical
type: regression
module: admin-portal
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:admin-platform, feat:notifications, issue:7340, r-2.0.9]
requirements: ["EliteaAI/elitea_issues#7340"]
---

# ELITEA-4884: Add toggle off suppresses added notification and on restores it

**Module:** admin-portal · **Priority:** critical · **Type:** regression

**Objective:** Regression of the add toggle: saving it off suppresses added notifications, saving it on restores them without restart. Manual source: ELITEA-4869.

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
| 1 | Turn the add toggle off and save | Setting saved. |
| 2 | As User A invite User B | Invite succeeds. |
| 3 | As User B open the popover | No added notification. |
| 4 | Remove User B, turn the add toggle on and save | Setting saved. |
| 5 | Invite User B again and open User B's popover | Added notification is present. |

---

## Expected Final State

Add toggle is on; one added notification from the second invite.

---

## Pass/Fail Criteria

**Pass:**
- No notification while off, one after turning on

**Fail:**
- Notification while off
- None after turning on
