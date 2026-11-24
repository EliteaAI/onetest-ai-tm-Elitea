---
id: ELITEA-4804
title: "External link opened by a viewer who is not logged in shows read-only content and enforces the password"
priority: critical
type: functional
module: conversations
status: draft
execution_type: manual
tags: [feat:chat, access-control, share-chat]
requirements: [EliteaAI/elitea_issues#7489]
---

# ELITEA-4804: External link opened by a viewer who is not logged in shows read-only content and enforces the password

**Module:** conversations · **Priority:** critical · **Type:** functional

**Objective:** Verify what a person outside the project sees when opening an external chat link, and the password flow.

---

## Preconditions

- User is logged in to `{{base_url}}`.
- User A owns chat C1 with at least 5 messages (text, code, markdown) and at least 2 attachments (image, document).
- Links from Share > Externally: L1 "All messages"; L2 "2 of N messages" with password; L3 "Attachments only".
- A browser window that is not logged in.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open L1 in the browser that is not logged in | The chat opens without login: chat name, all messages in order, markdown and code rendered, attachments listed |
| 2 | Look for controls | No message input, no Participants panel, no chat menu; nothing can be changed |
| 3 | Open or download an attachment | The file opens or downloads correctly |
| 4 | Open L2 and enter a wrong password | Access is denied with a clear message; no content; another try is possible |
| 5 | Enter the right password | Only the 2 selected messages and their files are shown |
| 6 | Open L3 | Only the attachments are shown, no message text |
| 7 | As User A, open Share > Externally | "Accessed <n> times" has grown for L1, L2 and L3 |

---

## Expected Final State

External viewers get read-only content limited to the link scope; the password is enforced.
