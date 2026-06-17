---
id: ELITEA-0468
title: "Verify Health Indicator When Adding Toolkit to Existing Conversation"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [credential-validation, toolkit-management, participants-panel, health-indicator, ux-improvement, chat-ui, 3709]
requirements: [GitHub Issue EliteaAI/elitea_issues#3709]
---
# ELITEA-0468: Verify Health Indicator When Adding Toolkit to Existing Conversation

**Module:** Chat Interface · **Priority:** High · **Type:** Functional

**Objective:** Verify that health indicator appears immediately when a user adds a misconfigured toolkit to an already existing conversation with message history.

**Coverage:**
- Dynamic health indicator addition
- Mid-conversation toolkit addition behavior
- Health indicator in existing conversation context
- Immediate indicator visibility on toolkit addition

## Preconditions

- User is logged in to ELITEA platform at {{base_url}}
- User has an existing conversation with message history (messages already exchanged)
- User has access to add toolkit participants to the conversation
- User has access to at least one misconfigured toolkit

## Test Data

- ELITEA URL: {{base_url}}
- Existing conversation: Conversation with existing message history
- Misconfigured toolkit: Toolkit participant with known configuration errors
- Expected behavior: Health indicator appears immediately after toolkit addition
- Conversation state: Active conversation with previous messages

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to an existing conversation that already has message history. | Existing conversation opens displaying previous message history in the chat area. |
| 2 | Note the current participants in the conversation before adding new toolkit. | Current participants are visible in the participants panel. Misconfigured toolkit is not yet added. |
| 3 | Add a misconfigured toolkit participant to the existing conversation via participants panel or toolkit selection. | Misconfigured toolkit is successfully added and appears in the participants panel alongside existing participants. |
| 4 | Immediately observe the newly added toolkit participant area (before sending any new messages). | Health indicator (yellow/orange icon) appears immediately next to the newly added toolkit participant name. |
| 5 | Verify the complete error message is displayed for the newly added toolkit. | Complete error message 'Misconfiguration errors found. Check the toolkit' is displayed below the toolkit name, with 'Check the toolkit' portion styled as an inline clickable link, without requiring any new message to be sent. |

## Expected Final State

Complete error message 'Misconfiguration errors found. Check the toolkit' is displayed below the toolkit name, with 'Check the toolkit' portion styled as an inline clickable link, without requiring any new message to be sent.

## Pass/Fail Criteria

**Pass:**
- Health indicator appears immediately when misconfigured toolkit is added to existing conversation
- Complete error message with clickable link is displayed right after toolkit addition
- No new messages need to be sent for indicator to appear
- Indicator integrates properly into existing conversation interface
- Existing message history is not affected by toolkit addition

**Fail:**
- Health indicator does not appear immediately after adding toolkit
- Error message appears only after sending a new message
- Indicator is delayed or requires conversation refresh
- Existing conversation state interferes with indicator display
- Health indicator fails to appear in mid-conversation toolkit addition
