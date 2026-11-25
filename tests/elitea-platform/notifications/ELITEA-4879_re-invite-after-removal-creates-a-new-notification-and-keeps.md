---
id: ELITEA-4879
title: "Re-invite after removal creates a new notification and keeps history"
priority: high
type: functional
module: notifications
status: draft
execution_type: manual
tags: [feat:admin-platform, feat:notifications, issue:7340, r-2.0.9]
requirements: ["EliteaAI/elitea_issues#7340"]
---

# ELITEA-4879: Re-invite after removal creates a new notification and keeps history

**Module:** notifications · **Priority:** high · **Type:** functional

**Objective:** Verify invite → remove → re-invite produces a new added notification while earlier notifications are kept.

---

## Preconditions

- User is logged in to `{{base_url}}`.
- Both toggles are on.
- User A is an admin of team project `mariam_test`; User B is logged in to `{{base_url}}` in a second browser profile.
- User B is not a member of `mariam_test`.

---

## Test Data

| Field | Value |
|-------|-------|
| Sequence | invite → remove → invite |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As User A invite User B | User B gets an added notification. |
| 2 | Remove User B | User B gets a removal notification. |
| 3 | Invite User B again | User B gets a new added notification. |
| 4 | As User B open Settings → Notifications | 3 notifications listed, newest first: added, removed, added. |

---

## Expected Final State

User B's full notification history is kept.

---

## Pass/Fail Criteria

**Pass:**
- All 3 notifications present, none overwritten

**Fail:**
- An earlier notification is missing
- Re-invite creates none
