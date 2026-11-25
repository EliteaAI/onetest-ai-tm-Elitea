---
id: ELITEA-4872
title: "Ghost user cleanup sends no project removal notification"
priority: critical
type: functional
module: notifications
status: draft
execution_type: manual
tags: [feat:admin-platform, feat:notifications, issue:7340, r-2.0.9]
requirements: ["EliteaAI/elitea_issues#7340"]
---

# ELITEA-4872: Ghost user cleanup sends no project removal notification

**Module:** notifications · **Priority:** critical · **Type:** functional

**Objective:** Verify the ghost-user cleanup task removes users without creating removal notifications.

---

## Preconditions

- User is logged in to `{{base_url}}`.
- Remove toggle is on and saved.
- A team project contains a ghost user; a dev can trigger the ghost-user cleanup task.

---

## Test Data

| Field | Value |
|-------|-------|
| Task | Ghost-user cleanup (`admin/tasks/project_tasks.py`) |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Note the ghost user's id and project | Ghost user is listed in the project. |
| 2 | Ask a dev to trigger the ghost-user cleanup | Task completes; ghost user is removed. |
| 3 | Query notifications for the ghost user's id with the removal event type | No removal notification exists. |

---

## Expected Final State

Ghost user is removed with no notification.

---

## Pass/Fail Criteria

**Pass:**
- Zero removal notifications

**Fail:**
- Cleanup creates a removal notification
