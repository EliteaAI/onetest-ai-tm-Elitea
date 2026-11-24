---
id: ELITEA-4797
title: "Share Chat Team tab copy link toasts and unsaved changes warning"
priority: high
type: functional
module: conversations
status: draft
execution_type: manual
tags: [feat:chat, access-control, share-chat]
requirements: [EliteaAI/elitea_issues#7489]
---

# ELITEA-4797: Share Chat Team tab copy link toasts and unsaved changes warning

**Module:** conversations · **Priority:** high · **Type:** functional

**Objective:** Verify the copy-link toasts of the Team tab and the warning on leaving with unsaved changes.

---

## Preconditions

- User is logged in to `{{base_url}}`.
- Team project; User A owns chat C1 with only the owner; User B is a project member.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open Share > Team and click the copy-link icon (tooltip "Copy link") | Toast "Link copied. Only you can access it for now." The URL is in the clipboard |
| 2 | Add User B without saving and click copy-link | Toast "Link copied. Save changes to grant access to added people." |
| 3 | Switch to Externally and back to Team | The unsaved list (with User B) is kept |
| 4 | Click × of the window; repeat with Cancel | Warning "There are unsaved changes. Are you sure you want to leave?". Cancel keeps the window; Leave closes it without saving |
| 5 | Reopen Share, add User B, Save, click copy-link | Toast "Link copied. Only people with access can open it." |

---

## Expected Final State

Toasts match the access state; unsaved changes are never lost silently.
