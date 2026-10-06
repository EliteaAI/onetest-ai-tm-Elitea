---
id: ELITEA-2074
title: "Chat – Create Agent with AI Build – Save Agent, Close Canvas, and Test with Conversation Starters"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2074: Chat – Create Agent with AI Build – Save Agent, Close Canvas, and Test with Conversation Starters

**Module:** chat-interface · **Priority:** high · **Type:** functional

**Objective:** Verify that after generating an agent using "Build with AI", the agent can be saved and closed, and that the generated conversation starters are displayed and functional in the conversation view.

---

## Preconditions

- User is logged in to the Elitea platform.
- An agent has been generated using "Build with AI" (following ELITEA-2073) and the canvas shows the "Echo Agent" configuration.

---

## Test Data

| Field | Value |
|-------|-------|
| Agent name | Echo Agent |
| Conversation starter 1 | Echo this: Hello, world! |
| Conversation starter 2 | Repeat this 3 times: test |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Verify the agent canvas shows the generated "Echo Agent" configuration with LLM model displayed | Canvas displays correctly with model chip |
| 2 | Scroll down to view WELCOME MESSAGE and CHAT STARTERS sections | Both sections are visible and populated |
| 3 | Verify four conversation starter buttons are displayed | All four starters are visible as dark buttons |
| 4 | Click the "Save" button in the top right corner of the canvas | Agent is saved successfully |
| 5 | Click the X button in the top right corner to close the canvas panel | Canvas closes; conversation view is displayed |
| 6 | Verify "Echo Agent" with version "base" is listed as an active participant in the message input area | Agent chip appears in message input area |
| 7 | Verify the four conversation starter buttons appear in the main conversation area | All four starters are visible below the greeting |
| 8 | Click on the first conversation starter "Echo this: Hello, world!" | Starter text is sent as a message |
| 9 | Verify the Echo Agent responds by echoing back exactly "Hello, world!" | Agent response appears attributed to "Echo Agent" |
| 10 | Click on "Repeat this 3 times: test" conversation starter | Starter text is sent as a message |
| 11 | Verify the agent responds by repeating "test" exactly 3 times | Agent response shows "test test test" |

---

## Expected Final State

The agent is saved, the canvas is closed, and all conversation starters are visible and functional in the conversation view. The agent executes correctly based on its generated instructions.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Agent saves, canvas closes, conversation starters are displayed and function as designed.

**Fail:**
- Any step produces an error or unexpected result.
- Starters are not displayed, agent does not respond correctly, or canvas does not close.
