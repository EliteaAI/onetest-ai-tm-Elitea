---
id: ELITEA-4461
title: "Export access requires chat visibility and a non-Viewer project role; Import access is governed by project-level permission, not visibility"
priority: critical
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:chat, chat-export, chat-import, permissions, feat:roles-permissions, bugfix, issue:6903, issue:6904, issue:7165, issue:7723, p0]
requirements: ["EliteaAI/elitea_issues#6903", "EliteaAI/elitea_issues#6904", "EliteaAI/elitea_issues#7165", "EliteaAI/elitea_issues#7723"]
---

# ELITEA-4461: Export access requires chat visibility and a non-Viewer project role; Import access is governed by project-level permission, not visibility

**Module:** chat-interface · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that Export is available only to users who can see the chat and whose project role is Editor or Admin (Viewer participants get no Export — bug #7723 fix), and that Import access depends only on the project-level `models.chat.conversations.create` permission (not any chat's visibility) — bug #7165 fix.

---

## Preconditions

- Two accounts: an Admin/owner account ("User A"), and a second test account ("User B") whose project role can be switched between Viewer/Editor/Admin.
- As User A, create three chats:
  1. A chat with any first message, shared with the Whole team via "⋮" > Share > Team (the "team chat").
  2. A chat with any first message, shared with selected people via "⋮" > Share > Team, with User B selected (the "private, added" chat).
  3. A chat with any first message, not shared, with User B never added to it (the "private, not added" chat).

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Set User B's role to Viewer. Log in as User B, check the chat list. | The team chat and the private-added chat are both visible/openable. The private-not-added chat does not appear at all in the list. |
| 2 | As User B (Viewer), open the team chat and open its "⋮" menu. | Export is not shown. The Export chat window cannot be opened. |
| 3 | As User B (Viewer), repeat step 2 for the private-added chat. | Export is not shown. The Export chat window cannot be opened. |
| 4 | Set User B's role to Editor and reload. As User B, export the team chat and the private-added chat — both "Without attachments" and "With attachments" (where the chat has attachments). | Export is shown in the "⋮" menu of both chats; all exports succeed. |
| 5 | Repeat step 4 with User B's role set to Admin. | Identical to step 4 — all exports succeed. |
| 6 | As User B, with role set to Viewer, then Editor, then Admin, check the Import button in the Chats header and complete a full import as each. | Import is visible/enabled and completes successfully for all three roles. |

## Expected Final State

Export access = "this user can see the chat" AND "this user's project role is Editor or Admin" (Viewer participants have no Export). Import access = project-level `models.chat.conversations.create` permission (independent of any chat's visibility).

## Pass/Fail Criteria

**Pass:**
- Viewer sees no Export on either visible chat; Editor and Admin export both visible chats; the not-added chat is invisible to every role; every role can import.

**Fail:**
- Export is shown to a Viewer or the Export chat window opens for a Viewer; Export is missing for Editor/Admin on a visible chat; or any role is blocked from import.
