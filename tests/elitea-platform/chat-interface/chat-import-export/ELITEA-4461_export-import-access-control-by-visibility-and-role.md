---
id: ELITEA-4461
title: "Export access is governed by chat visibility, not role; Import access is governed by project-level permission, not visibility"
priority: critical
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:chat, chat-export, chat-import, permissions, bugfix, issue:6903, issue:6904, issue:7165, p0]
requirements: ["EliteaAI/elitea_issues#6903", "EliteaAI/elitea_issues#6904", "EliteaAI/elitea_issues#7165"]
---

# ELITEA-4461: Export access is governed by chat visibility, not role; Import access is governed by project-level permission, not visibility

**Module:** chat-interface · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that Export access depends only on whether a user can see the chat (not their role), and Import access depends only on the project-level `models.chat.conversations.create` permission (not any chat's visibility) — bug #7165 fix.

---

## Preconditions

- Two accounts: an Admin/owner account ("User A"), and a second test account ("User B") whose project role can be switched between Viewer/Editor/Admin.
- As User A, create three chats:
  1. A chat with any first message. Use the "Make public" action on it so it is visible to all project members (the "public chat").
  2. A chat with any first message, kept private, with User B explicitly added as a participant (the "private, added" chat).
  3. A chat with any first message, kept private, with User B never added to it (the "private, not added" chat).

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Set User B's role to Viewer. Log in as User B, check the chat list. | The public chat and the private-added chat are both visible/openable. The private-not-added chat does not appear at all in the list. |
| 2 | As User B (Viewer), export the public chat — both "Without attachments" and "With attachments". | Both succeed. |
| 3 | As User B (Viewer), export the private-added chat — both modes. | Both succeed. |
| 4 | Repeat steps 1-3 with User B's role set to Editor, then to Admin. | Identical results for all three roles — no role-based restriction, only visibility matters. |
| 5 | As User B, with role set to Viewer, then Editor, then Admin, check the Import button in the Chats header and complete a full import as each. | Import is visible/enabled and completes successfully for all three roles. |

## Expected Final State

Export access = "can this user see the chat" (independent of role). Import access = project-level `models.chat.conversations.create` permission (independent of any chat's visibility).

## Pass/Fail Criteria

**Pass:**
- All roles export both visible chats identically; the not-added chat is invisible to every role; every role can import.

**Fail:**
- Any role-based export restriction, or any role blocked from import.
