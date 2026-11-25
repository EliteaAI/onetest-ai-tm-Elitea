---
id: ELITEA-4867
title: "Project name link in added notification opens the project Chats page"
priority: critical
type: functional
module: notifications
status: draft
execution_type: manual
tags: [feat:admin-platform, feat:notifications, issue:7340, r-2.0.9]
requirements: ["EliteaAI/elitea_issues#7340"]
---

# ELITEA-4867: Project name link in added notification opens the project Chats page

**Module:** notifications · **Priority:** critical · **Type:** functional

**Objective:** Verify only the project name is a link and clicking it switches the user to that project and opens its Chats page.

---

## Preconditions

- User is logged in to `{{base_url}}`.
- User B has an added notification for `mariam_test`.
- User B's current project is a different one (e.g. their private project).

---

## Test Data

| Field | Value |
|-------|-------|
| Project | `mariam_test` |
| Expected route | `{{base_url}}/app/<mariam_test projectId>/chat` |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As User B open the bell popover | Added notification is visible. |
| 2 | Hover over each part of the message | Only `mariam_test` is a link; "You have been added to" and "project." are plain text. |
| 3 | Click `mariam_test` | Project selector switches to `mariam_test`. |
| 4 | Check URL and page | URL is `/<projectId>/chat`; Chats page loads. |
| 5 | Switch to another project, open Settings → Notifications and click the link there | Same result as steps 3–4. |

---

## Expected Final State

User B is in `mariam_test` on its Chats page.

---

## Pass/Fail Criteria

**Pass:**
- Only the name is a link
- Link switches project and opens Chats from popover and View all

**Fail:**
- Other text is a link
- Link does nothing
- Wrong project or page opens
