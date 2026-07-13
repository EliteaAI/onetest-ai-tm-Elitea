---
id: ELITEA-1875
title: "Embedded chat — Shift+Enter inserts new line, Enter sends message"
priority: high
type: functional
module: agents
status: draft
execution_type: automated
tags: [automated:UI:regression, feat:agents]
requirements: []
---

# ELITEA-1875: Embedded chat — Shift+Enter inserts new line, Enter sends message

**Module:** agents · **Priority:** high · **Type:** functional

**Objective:** Verify that Shift+Enter inserts a new line without submitting the message, while Enter (without Shift) submits the message and triggers an agent response.

---

## Preconditions

- User is logged in to the Elitea platform.
- An existing agent with an embedded chat panel is available.

---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open an existing agent's detail page with an embedded chat panel | The agent detail page with embedded chat loads |
| 2 | Click the chat input field | The input field is focused |
| 3 | Press Shift+Enter — verify a new line is inserted and no message is sent | A new line appears in the input field; no message is submitted to the chat |
| 4 | Type additional text on the new line | The additional text appears on the new line in the input |
| 5 | Press Enter (without Shift) — verify the multi-line message is submitted | The multi-line message is sent to the chat |
| 6 | Verify an assistant response appears | An assistant response is rendered in the chat panel |

---

## Expected Final State

The chat shows the submitted multi-line message and an agent response. Shift+Enter correctly inserts line breaks without premature submission.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Shift+Enter inserts a new line; Enter submits the message and triggers a response.

**Fail:**
- Any step produces an error or unexpected result.
- Shift+Enter submits the message, or Enter does not submit and no response appears.
