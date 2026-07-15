---
id: ELITEA-2195
title: "Chat – File Attachments – Verify Attach Files Option Displays 10 Left Counter"
priority: medium
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2195: Chat – File Attachments – Verify Attach Files Option Displays 10 Left Counter

**Module:** chat-interface · **Priority:** medium · **Type:** functional

**Objective:** Verify that the 'Attach Files' option in the + menu shows a '10 left' counter indicating the maximum number of files.

---

## Preconditions

- User is logged in to the Elitea platform.
- User has an open conversation.

---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Navigate to Chats and open any conversation | Conversation open |
| 2 | Click the + icon at the bottom left of the message input area | Popup menu opens |
| 3 | Locate the 'Attach Files' option | 'Attach Files' displays '10 left' text on the right side |
| 4 | Verify the option has a paperclip/attachment icon on the left | Icon visible |
| 5 | Verify the option is clickable | Option clickable |

---

## Expected Final State

Attach Files shows '10 left' counter.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- '10 left' counter shown on Attach Files.

**Fail:**
- Any step produces an error or unexpected result.
- Counter missing or shows wrong value.
