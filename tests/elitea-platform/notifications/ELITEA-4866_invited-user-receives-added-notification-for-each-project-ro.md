---
id: ELITEA-4866
title: "Invited user receives added notification for each project role"
priority: critical
type: functional
module: notifications
status: draft
execution_type: manual
tags: [feat:admin-platform, feat:notifications, issue:7340, r-2.0.9]
requirements: ["EliteaAI/elitea_issues#7340"]
---

# ELITEA-4866: Invited user receives added notification for each project role

**Module:** notifications · **Priority:** critical · **Type:** functional

**Objective:** Verify a user invited via Settings → Users → Invite users gets exactly one "You have been added to <project> project." notification in any role.

---

## Preconditions

- User is logged in to `{{base_url}}`.
- Add toggle is on and saved.
- User A is an admin of team project `mariam_test`; User B is logged in to `{{base_url}}` in a second browser profile.
- User B is not a member of `mariam_test`.

---

## Test Data

| Field | Value |
|-------|-------|
| Run 1 role | viewer |
| Run 2 role | editor |
| Run 3 role | admin |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As User A open `mariam_test` → Settings → Users and click **+** | Invite users dialog opens. |
| 2 | Enter User B's email, select the role for this run, submit | User B appears in the Users list with that role. |
| 3 | As User B click the bell icon | Popover opens; bell shows the red unread dot. |
| 4 | Check the newest notification | Exactly one new notification: "You have been added to mariam_test project." with a relative time. |
| 5 | Open Settings → Notifications (View all) | The same notification is listed as unread. |
| 6 | As User A remove User B, then repeat steps 1–5 for the next role | Same results for every role. |

---

## Expected Final State

User B received exactly one added notification per invite in every role.

---

## Pass/Fail Criteria

**Pass:**
- One notification with correct text per role
- Shown in popover and View all

**Fail:**
- No notification or a duplicate
- Wrong text
- A role receives nothing
