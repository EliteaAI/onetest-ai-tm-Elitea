---
id: ELITEA-2174
title: "Chat – Team Project – Mention Two Users by Clicking Their Names in Participants Dropdown"
priority: medium
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2174: Chat – Team Project – Mention Two Users by Clicking Their Names in Participants Dropdown

**Module:** chat-interface · **Priority:** medium · **Type:** functional

**Objective:** Verify that clicking two users' names in the USERS dropdown inserts both @mentions into the message field.

---

## Preconditions

- User is logged in to the Elitea platform.
- A conversation with at least two added participants exists.

---

## Test Data

| Field | Value |
|-------|-------|
| Users | user_1, user_2 |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Open USERS dropdown, click on user_1's name | @user_1 inserted |
| 2 | Reopen USERS dropdown, click on user_2's name | @user_2 appended in message field |
| 3 | Type 'hi' and send '@user_1 @user_2 hi' | Message sent; both users notified; no LLM response |

---

## Expected Final State

Both @mentions inserted and sent; both users notified.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Two @mentions work correctly.

**Fail:**
- Any step produces an error or unexpected result.
- Mentions not inserted or LLM response triggered.
