---
id: ELITEA-4800
title: "Share for a user who is not the owner copies the link only; owner-only access changes are enforced"
priority: critical
type: functional
module: conversations
status: draft
execution_type: manual
tags: [feat:chat, access-control, share-chat]
requirements: [EliteaAI/elitea_issues#7489]
---

# ELITEA-4800: Share for a user who is not the owner copies the link only; owner-only access changes are enforced

**Module:** conversations · **Priority:** critical · **Type:** functional

**Objective:** Verify that for a user who is not the owner Share only copies the link and shows no external links, that the API rejects access changes by such a user, and that the personal project shows only the Externally content.

---

## Preconditions

- User is logged in to `{{base_url}}`.
- Team project; chat C1 owned by User A, shared with User B (selected people). User A has active external links on C1.
- An API client with the token of User B.
- User A has a chat in the personal project.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As User B, click Share in the chat menu and the Share button of the Users card | No window opens. The link is copied; toast "Link copied. Only people with access can open it." |
| 2 | As User B, check the Users card | No " · 🔗 n" count of external links |
| 3 | As User B, call the participants API to add another member, then the conversation API with `is_private: false` | Both requests are rejected (403 / access_denied). Access is unchanged |
| 4 | As User A, open Share on the chat in the personal project | No tabs and no copy-link button; the Externally content is shown under the header; a link can be created |

---

## Expected Final State

Only the owner can change access or see external links.

---

## Notes

- Step 3 depends on #7652.
- Q2 decision: users who are not the owner see neither the owner's links nor their count.
