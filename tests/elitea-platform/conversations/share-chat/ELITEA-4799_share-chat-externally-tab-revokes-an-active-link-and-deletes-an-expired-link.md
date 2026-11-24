---
id: ELITEA-4799
title: "Share Chat Externally tab revokes an active link and deletes an expired link"
priority: high
type: functional
module: conversations
status: draft
execution_type: manual
tags: [feat:chat, access-control, share-chat]
requirements: [EliteaAI/elitea_issues#7489]
---

# ELITEA-4799: Share Chat Externally tab revokes an active link and deletes an expired link

**Module:** conversations · **Priority:** high · **Type:** functional

**Objective:** Verify revoking active links and deleting expired links, and that a revoked link stops working.

---

## Preconditions

- User is logged in to `{{base_url}}`.
- User A owns chat C1 with at least 2 active external links and 1 expired link (a 1-hour link created more than 1 hour ago).
- A browser window that is not logged in.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open Share > Externally | "Active links – <n> · Expired – 1". Active cards first, newest first. The expired card has the orange badge "Expired", no expiry date and a delete button |
| 2 | Click Revoke on an active card, then Cancel | The link is kept |
| 3 | Click Revoke and confirm ("Revoke this link?" / "People who have this link will lose access. This can't be undone.") | Toast "Link revoked". The card disappears; counts update |
| 4 | Open the revoked link in the browser that is not logged in | Access is denied; no chat content |
| 5 | Delete the expired card | Toast "Link deleted". " · Expired" is gone from the heading |
| 6 | Revoke all active links | The tab shows the "Create link" form again; no count next to the tab name |

---

## Expected Final State

Revoked links give no access; the list and counts stay correct.

---

## Notes

- Expired link setup depends on #7653.
