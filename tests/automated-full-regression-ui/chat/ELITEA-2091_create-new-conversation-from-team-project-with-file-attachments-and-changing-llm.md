---
id: ELITEA-2091
title: "Create New Conversation from Team Project with File Attachments and changing LLM"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2091: Create New Conversation from Team Project with File Attachments and changing LLM

**Module:** chat-interface · **Priority:** high · **Type:** functional

**Objective:** Verify that in a Team project, a new conversation can be created with file attachments and a non-default LLM, and the conversation is auto-named after sending the first message.

---

## Preconditions

- User is logged in to the Elitea platform.
- User is in a Team project.

---

## Test Data

| Field | Value |
|-------|-------|
| First message | Please review the attached documents |
| Max file attachments | 10 |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Navigate to the Team project, go to Chats, and click + Chat | New blank conversation window opens |
| 2 | Click the + button below the message input field | Dropdown menu appears with Attach Files (with "10 left" counter), Modules, Agents, Pipelines, Toolkits, MCPs, Invite Users |
| 3 | Click "Attach Files" | File picker opens |
| 4 | Select up to 10 files and verify each file is listed; counter decrements with each file | Files attached; counter decrements correctly |
| 5 | Alternatively drag and drop one or more files and verify they appear as attachments | Dropped files appear identically to picker-selected files |
| 6 | Click on the LLM model selector | List of available LLMs opens |
| 7 | Select a different LLM from the dropdown | Selected LLM is shown with a checkmark |
| 8 | Type "Please review the attached documents" in the input field | Message entered |
| 9 | Click the Send button | Message and all attached files are submitted and appear in the chat thread |
| 10 | Verify a new conversation entry appears under "Today" with a "Naming…" placeholder that resolves to an auto-generated title | Conversation auto-named; response is generating |

---

## Expected Final State

Conversation created with file attachments and custom LLM; auto-named after first message is sent.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Files attach, LLM is changed, message sent, conversation auto-named.

**Fail:**
- Any step produces an error or unexpected result.
- Files fail to attach or auto-naming fails.
