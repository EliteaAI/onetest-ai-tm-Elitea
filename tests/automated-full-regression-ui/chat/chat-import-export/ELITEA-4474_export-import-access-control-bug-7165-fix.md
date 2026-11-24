---
id: ELITEA-4474
title: "Export is hidden for Viewer and available to Editor/Admin on visible chats; Import's role-based permission holds (bugs #7165, #7723)"
priority: critical
type: regression
module: chat-interface
status: draft
execution_type: manual
tags: [feat:chat, chat-export, chat-import, permissions, feat:roles-permissions, regression, issue:6903, issue:6904, issue:7165, issue:7723, p0]
requirements: ["EliteaAI/elitea_issues#6903", "EliteaAI/elitea_issues#6904", "EliteaAI/elitea_issues#7165", "EliteaAI/elitea_issues#7723"]
---

# ELITEA-4474: Export is hidden for Viewer and available to Editor/Admin on visible chats; Import's role-based permission holds (bugs #7165, #7723)

**Module:** chat-interface · **Priority:** Critical · **Type:** Regression

**Objective:** Confirm Export is available only on chats the user can see and only for the Editor/Admin project roles (not for Viewer participants), and Import remains governed purely by project-level permission (any role) — regression check for the bug #7165 and #7723 fixes.

---

## Preconditions

- As an Admin/owner account ("User A"), create: (1) a chat shared with the Whole team; (2) a chat shared with selected people, with a second test account ("User B") selected; (3) a chat User B is never added to.

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Set User B's role to Viewer. As User B, open the "⋮" menu of the Whole team chat and of the selected-people chat. | Export is not shown for either chat; the Export chat window cannot be opened. |
| 2 | Set User B's role to Editor, then Admin. For each role, export the Whole team chat and the selected-people chat (with/without attachments). | All exports succeed for each role. |
| 3 | As User B, check the chat list for the not-added chat. | Does not appear at all. |
| 4 | As User B, with role set to Viewer, then Editor, then Admin, confirm Import is enabled and completes successfully for each. | All succeed. |

## Expected Final State

Export requires chat visibility and an Editor/Admin role (no Export for Viewer); Import is governed purely by project permission (any role).

## Pass/Fail Criteria

**Pass:**
- All steps match exactly for every role.

**Fail:**
- Export available to a Viewer, Export missing for Editor/Admin on a visible chat, or any role blocked from import.
