---
id: ELITEA-4812
title: "Chat – External Chat Link Created, Opened Without Login with Password, Revoked and No Longer Works"
priority: critical
type: functional
module: conversations
status: draft
execution_type: manual
tags: [manual:UI:regression, feat:chat, share-chat]
requirements: [EliteaAI/elitea_issues#7489]
---

# ELITEA-4812: Chat – External Chat Link Created, Opened Without Login with Password, Revoked and No Longer Works

**Module:** conversations · **Priority:** critical · **Type:** functional

**Objective:** Verify the main external-link journey: create a link, open it without login (with and without password), revoke it and check that it no longer works.

---

## Preconditions

- User is logged in to the Elitea platform.
- User A owns chat C1 in a team project with at least 3 messages and at least 1 attachment.
- A browser window that is not logged in.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As User A, open Share > Externally, keep All messages with both checkboxes and 7 days, click Generate Link | Toast "Link created"; card "All N messages - Expires <date>"; the tab shows 1 |
| 2 | Copy the link and open it in the browser that is not logged in | Messages and the attachment of C1 are shown read-only, with no input or actions; no login is needed |
| 3 | As User A, create a second link: Selected messages (1 message), password of 8+ characters | A new card at the top with a lock icon |
| 4 | Open the second link: enter a wrong password, then the right one | The wrong password is rejected; the right one shows only the selected message |
| 5 | As User A, revoke the first link and confirm | Toast "Link revoked"; the card is gone; counts update |
| 6 | Reload the first link in the browser that is not logged in | Access is denied; no content |
| 7 | As User A, delete C1, then reload the second link | Access is denied; no content |

---

## Expected Final State

External links give scoped read-only access and stop working once revoked or when the chat is deleted.
