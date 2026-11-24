---
id: ELITEA-4798
title: "Share Chat Externally tab creates external links with different scopes, expiration and password"
priority: critical
type: functional
module: conversations
status: draft
execution_type: manual
tags: [feat:chat, access-control, share-chat]
requirements: [EliteaAI/elitea_issues#7489]
---

# ELITEA-4798: Share Chat Externally tab creates external links with different scopes, expiration and password

**Module:** conversations · **Priority:** critical · **Type:** functional

**Objective:** Verify the Create link form of the Externally tab: defaults, validation, scopes, expiration and password.

---

## Preconditions

- User is logged in to `{{base_url}}`.
- Team project; User A owns chat C1 with at least 5 messages and at least 2 attachments, with no external links.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open Share > Externally | Form "Create link": Messages – N and Attachments – M files checked, All messages, Link expiration 7 days, Password empty. M matches the number of files in the Export dialog |
| 2 | Uncheck both "What to include" checkboxes | Generate Link is disabled |
| 3 | Check Messages; enter a password of 1–7 characters | Error "Minimum 8 characters"; Generate Link is disabled. The eye shows/hides the password; copy works |
| 4 | Clear the password; keep All + Messages only, choose 1 hour, click Generate Link | Toast "Link created". The list shows the info banner, "Active links – 1" and the card "Messages only (N) - Expires <date>", "Accessed 0 times - Created <date>". The card is active, not Expired |
| 5 | Click Create Link, choose Selected messages, check 2 rows (click anywhere on a row) | Checkboxes read "Messages – 2 of N" and "Attachments – <f> of M files", checked and disabled. With 0 rows checked Generate Link is disabled |
| 6 | Enter a password of at least 8 characters, choose Never expires, click Generate Link | A new card at the top: "2 of N messages - Never expires" with a lock icon. The tab Externally shows the number of active links |

---

## Expected Final State

Links are created with the chosen scope, expiration and password and are listed newest first.

---

## Notes

- Step 4 depends on #7653 (1-hour link created as Expired).
