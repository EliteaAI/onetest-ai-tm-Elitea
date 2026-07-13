---
id: ELITEA-1885
title: "Welcome message is shown as agent bubble before first user message"
priority: medium
type: functional
module: agents
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:agents]
requirements: []
---

# ELITEA-1885: Welcome message is shown as agent bubble before first user message

**Module:** agents · **Priority:** medium · **Type:** functional

**Objective:** Verify that a configured welcome message is displayed as an agent bubble in the embedded chat panel before the user sends any message.

---

## Preconditions

- User is logged in to the Elitea platform.
- An existing agent is available.

---

## Test Data

| Field | Value |
|-------|-------|
| Welcome message | Welcome! I am your test assistant. How can I help you today? |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to an agent detail page | The agent detail page loads |
| 2 | Set welcome message: "Welcome! I am your test assistant. How can I help you today?" | The welcome message field displays the text |
| 3 | Click Save | Save completes successfully |
| 4 | Open the embedded chat panel (or start a new chat from the agent page) | The chat panel opens |
| 5 | Verify the welcome message is displayed before any user message is sent | The welcome message text is visible in the chat panel with no prior user messages |
| 6 | Verify the welcome message appears as an agent bubble (not a user bubble) | The welcome message is rendered with agent styling (e.g., on the left side or with agent avatar) |

---

## Expected Final State

The embedded chat panel shows the configured welcome message as an agent bubble before the user sends any message.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The welcome message is displayed as an agent bubble before the first user message.

**Fail:**
- Any step produces an error or unexpected result.
- The welcome message is absent, appears after user input, or is displayed as a user bubble.
