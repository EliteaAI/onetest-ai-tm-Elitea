---
id: ELITEA-4807
title: "Shared chat access and external links after rename, duplicate and delete"
priority: high
type: functional
module: conversations
status: draft
execution_type: manual
tags: [feat:chat, access-control, share-chat]
requirements: [EliteaAI/elitea_issues#7489]
---

# ELITEA-4807: Shared chat access and external links after rename, duplicate and delete

**Module:** conversations · **Priority:** high · **Type:** functional

**Objective:** Verify team access and external links of a shared chat after the chat is renamed, duplicated and deleted.

---

## Preconditions

- User is logged in to `{{base_url}}`.
- User A owns chat C1 shared with User B, with at least 1 active external link L1.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Rename C1 to a long name (80+ characters) | The Share window header shows the new name cut with "…"; L1 and User B show the new name |
| 2 | Duplicate C1 and open Share on the copy | The Externally tab of the copy has no links (Create link form); the Users card of the copy matches its access per the duplicate rules |
| 3 | Check Share of C1 | Access and L1 of C1 are unchanged |
| 4 | Delete C1 | C1 is removed |
| 5 | Open L1 in a browser that is not logged in; as User B open the URL of C1 | Both are denied cleanly; C1 is not in User B's list |

---

## Expected Final State

Rename, duplicate and delete keep access and links consistent.
