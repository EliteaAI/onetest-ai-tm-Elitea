---
id: ELITEA-2201
title: "Chat – File Attachments – Send Message with Attached Files and Verify Files Are Included"
priority: medium
type: functional
module: chat-interface
status: ready
execution_type: automated
automation_test_id: "tests.ui.chat.test_send_message_with_attachments_verify_included.TestSendMessageWithAttachmentsVerifyIncluded.test_send_message_with_attachments_verify_included"
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1595
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2201: Chat – File Attachments – Send Message with Attached Files and Verify Files Are Included

**Module:** chat-interface · **Priority:** medium · **Type:** functional

**Objective:** Verify that sending a message with attached files includes the files in the conversation and the LLM/agent acknowledges them.

---

## Preconditions

- User is logged in to the Elitea platform.
- User has an open conversation with an agent or LLM.

---

## Test Data

| Field | Value |
|-------|-------|
| Files | 3-4 supported files | Message | Please analyze these files |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Attach 3-4 supported files via + icon > Attach Files | Files uploaded and chips shown |
| 2 | Type 'Please analyze these files' in the input field | Message entered |
| 3 | Click Send | Message sent; file references included in conversation |
| 4 | Verify LLM/agent acknowledges and begins processing the files | Response references attached files |
| 5 | Verify after sending, attachment chips are cleared from input field | Chips cleared |

---

## Expected Final State

Files sent with message; LLM processes them; chips cleared after send.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Files sent and processed; chips cleared.

**Fail:**
- Any step produces an error or unexpected result.
- Files not sent or chips not cleared.
