---
id: ELITEA-2168
title: "Chat – Team Project – Add Multiple Users, Mention Users, View Users Dropdown and Remove Access"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat]
requirements: [EliteaAI/elitea_issues#7489]
---

# ELITEA-2168: Chat – Team Project – Add Multiple Users, Mention Users, View Users Dropdown and Remove Access

**Module:** chat-interface · **Priority:** high · **Type:** functional

**Objective:** Verify the complete flow of adding multiple users with deselection in the Share Chat window, mentioning users, using Everyone, and removing access via the Share Chat window.

---

## Preconditions

- User is logged in to the Elitea platform.
- User is the owner of an existing conversation in a Team project.

---

## Test Data

| Field | Value |
|-------|-------|
| Users | user_1, user_2, user_3, user_4 | Mention | @Test Bot hi | @Everyone message | @Everyone hi |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Open the conversation in Team project | PARTICIPANTS panel with the Users card visible |
| 2 | Open Share > Team; in the search dropdown pick user_1, user_2, user_3, user_4, then click user_4 again | user_4 unchecked; "3 selected" |
| 3 | Click Add, then Save | user_1/2/3 listed; Users card shows "N users" (owner included) |
| 4 | Click "N users" on the Users card | Dropdown: Everyone, own row "(You)" (not clickable), then the people, owner first with the badge "Owner" |
| 5 | Type '@Test Bot hi' and send | Message sent; notification badge appears; no LLM response generated |
| 6 | Hover a person in the users dropdown | Only "@" is shown; no delete icon |
| 7 | Open Share > Team, hover user_1, click ×, then Save | user_1 removed; card count −1; user_1 not in the dropdown |
| 8 | Open Share > Team, hover user_2, click ×, then Cancel and Leave | user_2 keeps access |
| 9 | Click "Everyone" in the users dropdown | @Everyone inserted and highlighted in the message field |
| 10 | Type 'hi' and send '@Everyone hi' | Message sent; all people with access receive notification; no LLM response |

---

## Expected Final State

Multiple users managed via Share Chat; @mention and Everyone work; access removal via Share Chat works.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- All user management flows work correctly.

**Fail:**
- Any step produces an error or unexpected result.
- User add/remove fails or mentions don't work.
