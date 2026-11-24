---
id: ELITEA-4801
title: "Participants panel Users card states and users dropdown with mentions"
priority: high
type: functional
module: conversations
status: draft
execution_type: manual
tags: [feat:chat, access-control, share-chat]
requirements: [EliteaAI/elitea_issues#7489]
---

# ELITEA-4801: Participants panel Users card states and users dropdown with mentions

**Module:** conversations · **Priority:** high · **Type:** functional

**Objective:** Verify the Users card of the Participants panel (who can open the chat, number of external links) and its users dropdown used for mentions.

---

## Preconditions

- User is logged in to `{{base_url}}`.
- Team project with at least 10 members.
- Chats owned by User A: C1 (only the owner, 2 active links and 1 expired), C2 (5 selected people incl. User B), C3 (Whole team).
- User D is a project member who has never opened C3.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As User A, open C1, C2 and C3 in turn | Users card: a lock and "Only You · 🔗 2" (tooltip "2 active external links · 1 expired"); "5 users"; "Whole Team (N)" — counts include the owner. "5 users" and "Whole Team (N)" are underlined and take the primary colour on hover; "Only You" is plain text |
| 2 | Hover the card on C2 and click the Share icon | As User A the Share Chat window opens; as User B the link is copied with a toast |
| 3 | As User B, click "5 users" on C2 | Dropdown under the card: Everyone, then User B with a grey "(You)" (no "@", no hover, not clickable), then the people with User A first and the badge "Owner". No delete |
| 4 | As User A, open the same dropdown | User A's own row shows "(You)" right under Everyone |
| 5 | On C3, open the dropdown | From 9 people up the search "Search user …" is shown and filters the list |
| 6 | Click the row of User D (shows "@" on hover) and send the message; then click Everyone | A mention of User D is inserted and sent without errors; User D becomes a participant. Everyone inserts @Everyone |
| 7 | Change access in the Share window and Save | The card updates without reload |

---

## Expected Final State

The Users card shows who can open the chat; the dropdown mentions follow the rules of #7489 item 8.

---

## Notes

- Q1 decision: mentions go by project user id; the server adds the participant (#7523).
