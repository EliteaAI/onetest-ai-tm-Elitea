---
id: ELITEA-4877
title: "Role change of an existing member sends no membership notification"
priority: high
type: functional
module: notifications
status: draft
execution_type: manual
tags: [feat:admin-platform, feat:notifications, issue:7340, r-2.0.9]
requirements: ["EliteaAI/elitea_issues#7340"]
---

# ELITEA-4877: Role change of an existing member sends no membership notification

**Module:** notifications · **Priority:** high · **Type:** functional

**Objective:** Verify changing roles of existing members, single or batch, does not create membership notifications.

---

## Preconditions

- User is logged in to `{{base_url}}`.
- Both toggles are on.
- Users B and C are viewer members of `mariam_test`.

---

## Test Data

| Field | Value |
|-------|-------|
| Single (B) | viewer → editor |
| Batch (B, C) | → admin |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As User A open Edit roles for User B, change viewer → editor, save | Role updated. |
| 2 | Select B and C, batch edit roles to admin, save | Roles updated. |
| 3 | As User B and User C open the popover | No new added or removal notification. |

---

## Expected Final State

Roles changed; no notifications created.

---

## Pass/Fail Criteria

**Pass:**
- Zero membership notifications

**Fail:**
- Any notification after a role change
