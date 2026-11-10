---
id: ELITEA-4474
title: "Export visibility-based access and Import's role-based permission both hold (bug #7165 fix)"
priority: critical
type: regression
module: chat-interface
status: draft
execution_type: manual
tags: [feat:chat, chat-export, chat-import, permissions, regression, issue:6903, issue:6904, issue:7165, p0]
requirements: ["EliteaAI/elitea_issues#6903", "EliteaAI/elitea_issues#6904", "EliteaAI/elitea_issues#7165"]
---

# ELITEA-4474: Export visibility-based access and Import's role-based permission both hold (bug #7165 fix)

**Module:** chat-interface · **Priority:** Critical · **Type:** Regression

**Objective:** Confirm Export remains governed purely by chat visibility (any role), and Import remains governed purely by project-level permission (any role) — regression check for the bug #7165 fix.

---

## Preconditions

- As an Admin/owner account ("User A"), create: (1) a chat made public via "Make public"; (2) a private chat with a second test account ("User B") explicitly added as a participant; (3) a private chat User B is never added to.

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Set User B's role to Viewer. Export the public chat and the private-added chat (both with/without attachments). | All 4 exports succeed. |
| 2 | As User B, check the chat list for the private-not-added chat. | Does not appear at all. |
| 3 | As User B, with role set to Viewer, then Editor, then Admin, confirm Import is enabled and completes successfully for each. | All succeed. |

## Expected Final State

Export is governed purely by visibility (any role); Import purely by project permission (any role).

## Pass/Fail Criteria

**Pass:**
- All steps match exactly for every role.

**Fail:**
- Any role-based export restriction, or any role blocked from import.
