---
id: ELITEA-2205
title: "Chat – Slash Commands – Verify Selecting MCP from / Dropdown"
priority: medium
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2205: Chat – Slash Commands – Verify Selecting MCP from / Dropdown

**Module:** chat-interface · **Priority:** medium · **Type:** functional

**Objective:** Verify that selecting an MCP from the '/' dropdown adds it to the message field.

---

## Preconditions

- User is logged in to the Elitea platform.
- Conversation with MCP 'delete' added as participant.

---

## Test Data

| Field | Value |
|-------|-------|
| MCP name | delete |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Type '/' and click 'delete' in dropdown | Message field shows '/delete' |
| 2 | Verify if MCP has tools, they are displayed; if no tools/disconnected, no tools list | Tools shown or no tools depending on MCP state |

---

## Expected Final State

MCP selectable via '/' command.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- MCP shows in '/' dropdown and can be selected.

**Fail:**
- Any step produces an error or unexpected result.
- MCP not in dropdown or not selectable.
