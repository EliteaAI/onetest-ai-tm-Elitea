---
id: ELITEA-2180
title: "Chat – Edit Last User Message – Cancel Discards Changes Then Save and Apply Saves Changes"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2180: Chat – Edit Last User Message – Cancel Discards Changes Then Save and Apply Saves Changes

**Module:** chat-interface · **Priority:** high · **Type:** functional

**Objective:** Verify that editing the last user message, cancelling discards the change, and clicking 'Save and apply' replaces the message and triggers a new LLM response.

---

## Preconditions

- User is logged in to the Elitea platform.
- A conversation with at least one user message and LLM response exists.

---

## Test Data

| Field | Value |
|-------|-------|
| Edited message 1 | this is a changed message | Edited message 2 | explain bubble sort instead |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Hover over the last user message; verify pencil and copy icons appear | Icons visible |
| 2 | Hover over pencil; verify tooltip 'Edit the message and regenerate answer' | Tooltip correct |
| 3 | Click pencil icon | Message in editable text area with current text pre-filled; Cancel and 'Save and apply' buttons shown |
| 4 | Clear text and type 'this is a changed message'; verify 'Save and apply' active | Button active |
| 5 | Click Cancel | Edit mode closes; original message restored; no new LLM response triggered |
| 6 | Click pencil icon again, clear and type 'explain bubble sort instead' | New text in edit area |
| 7 | Click 'Save and apply' | Edited message replaces original; previous LLM response removed; new response generated |

---

## Expected Final State

Cancel preserves original; Save and apply replaces message and triggers new response.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Edit, cancel, and save and apply all work correctly.

**Fail:**
- Any step produces an error or unexpected result.
- Cancel saves changes or save and apply fails.
