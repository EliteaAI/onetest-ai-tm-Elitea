---
id: ELITEA-4876
title: "Multi-select removal sends one notification per removed user"
priority: high
type: functional
module: notifications
status: draft
execution_type: manual
tags: [feat:admin-platform, feat:notifications, issue:7340, r-2.0.9]
requirements: ["EliteaAI/elitea_issues#7340"]
---

# ELITEA-4876: Multi-select removal sends one notification per removed user

**Module:** notifications · **Priority:** high · **Type:** functional

**Objective:** Verify a batch removal sends exactly one removal notification to each removed user.

---

## Preconditions

- User is logged in to `{{base_url}}`.
- Remove toggle is on.
- Users B, C and D are members of `mariam_test`.

---

## Test Data

| Field | Value |
|-------|-------|
| Users | B, C, D |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As User A open Settings → Users and select B, C and D | Toolbar delete icon is enabled. |
| 2 | Click delete and confirm | All three are removed; DELETE returns `204` in DevTools. |
| 3 | As B, C and D in turn open the popover | Each has exactly one removal notification. |
| 4 | As User A open the popover | No removal notification. |

---

## Expected Final State

Three removal notifications, one per user.

---

## Pass/Fail Criteria

**Pass:**
- One notification each for B, C, D
- Response `204`

**Fail:**
- Missing or duplicate notification
- Error response
