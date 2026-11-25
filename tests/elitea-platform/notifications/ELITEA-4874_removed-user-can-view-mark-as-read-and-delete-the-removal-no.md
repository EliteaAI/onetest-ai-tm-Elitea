---
id: ELITEA-4874
title: "Removed user can view mark as read and delete the removal notification"
priority: high
type: functional
module: notifications
status: draft
execution_type: manual
tags: [feat:admin-platform, feat:notifications, issue:7340, r-2.0.9]
requirements: ["EliteaAI/elitea_issues#7340"]
---

# ELITEA-4874: Removed user can view mark as read and delete the removal notification

**Module:** notifications · **Priority:** high · **Type:** functional

**Objective:** Verify a user who lost project access can still view, mark as read and delete the removal notification, and changes persist.

---

## Preconditions

- User is logged in to `{{base_url}}`.
- User B has an unread removal notification for `mariam_test` and is no longer a member.

---

## Test Data

| Field | Value |
|-------|-------|
| Page | `{{base_url}}/app/` → Settings → Notifications |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As User B open the popover and View all | Removal notification is listed in both. |
| 2 | Mark it as read via the envelope icon | Unread state clears. |
| 3 | Reload the page | It is still read. |
| 4 | In View all select it and delete | It disappears from the list. |
| 5 | Reload the page | It does not reappear. |
| 6 | Check PUT and DELETE responses in DevTools | Both succeed (no 403 or 404). |

---

## Expected Final State

The removal notification is deleted.

---

## Pass/Fail Criteria

**Pass:**
- View, mark read and delete work
- Each change survives a reload

**Fail:**
- Any action errors
- Change reverts after reload
