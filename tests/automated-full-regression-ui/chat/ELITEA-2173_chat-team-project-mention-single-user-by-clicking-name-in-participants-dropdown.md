---
id: ELITEA-2173
title: "Chat – Team Project – Mention Single User by Clicking Name in Participants Dropdown"
priority: medium
type: functional
module: chat-interface
status: ready
execution_type: automated
automation_test_id:
  - tests.ui.chat.test_participants_dropdown_click_name_inserts_mention.TestParticipantsDropdownClickNameInsertsMention.test_click_participant_name_inserts_mention[ELITEA-2173-single-mention]
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1561
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2173: Chat – Team Project – Mention Single User by Clicking Name in Participants Dropdown

**Module:** chat-interface · **Priority:** medium · **Type:** functional

**Objective:** Verify that clicking a user's name in the USERS dropdown inserts an @mention into the message field.

---

## Preconditions

- User is logged in to the Elitea platform.
- A conversation with at least one added participant exists.

---

## Test Data

| Field | Value |
|-------|-------|
| User | user_1 | Message suffix | hi |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Open conversation, click avatar group to open USERS dropdown | Dropdown shows participants |
| 2 | Click on user_1's name | @user_1 inserted into message input field |
| 3 | Verify mention is highlighted/formatted | Mention highlighted |
| 4 | Type 'hi' and send '@user_1 hi' | Message sent; user_1 receives notification; no LLM response generated |

---

## Expected Final State

@mention inserted and sent; user_1 notified.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Mention works; user notified.

**Fail:**
- Any step produces an error or unexpected result.
- Mention not inserted or LLM response triggered.
