---
id: ELITEA-4883
title: "Removed user receives plain-text removal notification when enabled"
priority: critical
type: regression
module: notifications
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:admin-platform, feat:notifications, issue:7340, r-2.0.9]
requirements: ["EliteaAI/elitea_issues#7340"]
---

# ELITEA-4883: Removed user receives plain-text removal notification when enabled

**Module:** notifications · **Priority:** critical · **Type:** regression

**Objective:** Regression of the removal notification: with the remove toggle on, a removed user gets one plain-text notification with no link. Manual source: ELITEA-4868, ELITEA-4870.

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
| 1 | As User A delete User B on `mariam_test` → Settings → Users | User B is removed. |
| 2 | As User B open the bell popover | One notification "You have been removed from mariam_test project." |
| 3 | Hover and click the project name | Nothing is a link; no navigation. |

---

## Expected Final State

User B has one plain-text removal notification.

---

## Pass/Fail Criteria

**Pass:**
- One removal notification, no link

**Fail:**
- No notification
- Project name is clickable
