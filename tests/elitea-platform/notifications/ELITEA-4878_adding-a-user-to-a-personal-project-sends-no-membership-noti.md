---
id: ELITEA-4878
title: "Adding a user to a personal project sends no membership notification"
priority: high
type: functional
module: notifications
status: draft
execution_type: manual
tags: [feat:admin-platform, feat:notifications, issue:7340, r-2.0.9]
requirements: ["EliteaAI/elitea_issues#7340"]
---

# ELITEA-4878: Adding a user to a personal project sends no membership notification

**Module:** notifications · **Priority:** high · **Type:** functional

**Objective:** Verify membership notifications are never created for personal (private) projects.

---

## Preconditions

- User is logged in to `{{base_url}}`.
- Add toggle is on.
- User A has a personal (private) project.

---

## Test Data

| Field | Value |
|-------|-------|
| Project | User A's private project id |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Attempt to add User B to User A's private project via UI, or via `POST admin/api/v2/users` if the UI blocks it | Request is handled (rejected or accepted). |
| 2 | As User B check the popover and `GET` notifications API | No added notification for the private project. |

---

## Expected Final State

No membership notification exists for the personal project.

---

## Pass/Fail Criteria

**Pass:**
- Zero notifications

**Fail:**
- Added notification referencing the private project
