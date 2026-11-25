---
id: ELITEA-4882
title: "Invited user receives added notification and link opens project Chats"
priority: critical
type: regression
module: notifications
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:admin-platform, feat:notifications, issue:7340, r-2.0.9]
requirements: ["EliteaAI/elitea_issues#7340"]
---

# ELITEA-4882: Invited user receives added notification and link opens project Chats

**Module:** notifications · **Priority:** critical · **Type:** regression

**Objective:** Regression of the added notification: an invited user gets one "You have been added to <project> project." notification and the project-name link opens the project's Chats page. Manual source: ELITEA-4866, ELITEA-4867.

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
| Project | `mariam_test` |
| Role | viewer |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As User A invite User B to `mariam_test` as viewer | User B appears in the Users list. |
| 2 | As User B open the bell popover | Unread dot shown; one notification "You have been added to mariam_test project." |
| 3 | Hover the message | Only `mariam_test` is a link. |
| 4 | Click `mariam_test` | Project switches to `mariam_test`; URL is `/<projectId>/chat`; Chats page loads. |

---

## Expected Final State

User B is on `mariam_test` Chats with the notification received.

---

## Pass/Fail Criteria

**Pass:**
- One added notification with correct text
- Link opens the project Chats

**Fail:**
- No or duplicate notification
- Link missing or wrong target
