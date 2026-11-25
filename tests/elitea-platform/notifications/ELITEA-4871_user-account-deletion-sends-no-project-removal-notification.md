---
id: ELITEA-4871
title: "User account deletion sends no project removal notification"
priority: critical
type: functional
module: notifications
status: draft
execution_type: manual
tags: [feat:admin-platform, feat:notifications, issue:7340, r-2.0.9]
requirements: ["EliteaAI/elitea_issues#7340"]
---

# ELITEA-4871: User account deletion sends no project removal notification

**Module:** notifications · **Priority:** critical · **Type:** functional

**Objective:** Verify the user-deletion cascade removes the user from team projects without creating removal notifications.

---

## Preconditions

- User is logged in to `{{base_url}}`.
- Logged in to `{{base_url}}` as a platform admin with access to the Admin portal.
- Remove toggle is on and saved.
- Throwaway User T is a member of `mariam_test` and one other team project.

---

## Test Data

| Field | Value |
|-------|-------|
| User | User T (throwaway) |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As the platform admin open Admin → People & Access and delete User T's account | Account is deleted. |
| 2 | Check the Users lists of `mariam_test` and the other project | User T no longer appears. |
| 3 | Query notifications for User T's id with the removal event type (DB or dev) | No removal notification exists for either project. |

---

## Expected Final State

User T is deleted and no removal notifications were created.

---

## Pass/Fail Criteria

**Pass:**
- Zero removal notifications for User T

**Fail:**
- Any removal notification created by the deletion cascade
