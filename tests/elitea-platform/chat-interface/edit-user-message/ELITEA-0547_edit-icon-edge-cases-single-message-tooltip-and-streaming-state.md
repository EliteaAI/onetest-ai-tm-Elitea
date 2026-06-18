---
id: ELITEA-0547
title: "Edit icon edge cases — single message, tooltip, and streaming state"
priority: high
type: functional
module: edit-user-message
status: ready
execution_type: manual
tags: [feat:chat, r-2.0.4]
requirements: [EliteaAI/elitea_issues#4942]
---
# ELITEA-0547: Edit icon edge cases — single message, tooltip, and streaming state

**Module:** Edit User Message · **Priority:** High · **Type:** Functional

**Objective:** Verify Edit icon behavior in boundary scenarios: single-message conversation, tooltip text, and during active LLM streaming.

**Coverage:**
- Icon visible when only one user message exists
- Tooltip reads "Edit"
- Icon behavior during LLM response streaming

## Preconditions

- User is logged in to ELITEA at {{base_url}}
- Browser: Chrome latest
- Ability to start a new empty conversation

## Test Data

- First message: "Write me a 500-word essay on climate change" (long enough to observe streaming)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Start a new Chat Conversation. Send the first message: "Write me a 500-word essay on climate change". | Message is sent. LLM begins streaming a response. |
| 2 | While the LLM response is still being generated (streaming), check if the Edit icon is visible on the user message. | Edit icon is either hidden or disabled during streaming (not clickable). |
| 3 | Wait for the LLM response to complete. Check for the Edit icon on the single user message. | Edit icon is visible on the only user message in the conversation. |
| 4 | Hover over the Edit icon. | Tooltip text reads exactly "Edit the message and regenerate answer". |

## Expected Final State

Tooltip text reads exactly "Edit the message and regenerate answer".

## Pass/Fail Criteria

**Pass:**
- Edit icon is present on a single-message conversation after response completes
- Tooltip text is "Edit"
- Icon is not actionable during streaming

**Fail:**
- Edit icon missing on single user message
- Tooltip text is incorrect or missing
- User can click Edit while LLM is still streaming
