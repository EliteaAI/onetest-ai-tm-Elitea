---
id: ELITEA-0458
title: "Verify Health Indicator for Newly Created Chat Before Messages"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [credential-validation, toolkit-management, participants-panel, health-indicator, ux-improvement, chat-ui, 3709]
requirements: [GitHub Issue #3709]
---
# ELITEA-0458: Verify Health Indicator for Newly Created Chat Before Messages

**Module:** Chat Interface · **Priority:** High · **Type:** Functional

**Objective:** Verify that health indicator appears for a newly created chat when a misconfigured toolkit is added before any messages are sent.

**Coverage:**
- Immediate health indicator display on toolkit addition
- Pre-conversation health indicator functionality
- New chat initialization with misconfigured toolkit
- Early warning before message exchange

## Preconditions

- User is logged in to ELITEA platform at {{base_url}}
- User has access to create new chats/conversations
- User has access to at least one misconfigured toolkit
- No messages have been sent in the new chat yet

## Test Data

- ELITEA URL: {{base_url}}
- New chat: Freshly created conversation with no message history
- Misconfigured toolkit: Toolkit participant with known configuration errors
- Expected behavior: Health indicator appears immediately upon adding misconfigured toolkit
- Message count: Zero messages in conversation

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Create a new chat/conversation in ELITEA platform. | New chat is created and opened with empty conversation area (no messages displayed). |
| 2 | Add a misconfigured toolkit participant to the newly created chat via participants panel or toolkit selection. | Misconfigured toolkit is successfully added to the conversation and appears in the participants panel. |
| 3 | Observe the toolkit participant area immediately after addition, before sending any messages. | Health indicator (yellow/orange icon) appears immediately next to the toolkit participant name, without needing to send a message. |
| 4 | Verify the complete error message is displayed below the toolkit name. | Complete error message 'Misconfiguration errors found. Check the toolkit' is displayed with 'Check the toolkit' portion styled as an inline clickable link. |
| 5 | Confirm no messages have been sent in the conversation yet. | Conversation message area is empty. Health indicator and error message are visible even though no conversation interaction has occurred. |

## Expected Final State

Conversation message area is empty. Health indicator and error message are visible even though no conversation interaction has occurred.

## Pass/Fail Criteria

**Pass:**
- Health indicator appears immediately upon adding misconfigured toolkit to new chat
- Complete error message with clickable link is displayed before any messages are sent
- Indicator and message are visible in empty conversation (no messages required)
- Early warning is provided to user before they attempt to use the misconfigured toolkit

**Fail:**
- Health indicator does not appear until after a message is sent
- Error message is delayed or missing in new chat
- User must interact with conversation before indicator appears
- Indicator only shows after conversation is created (not immediately on toolkit addition)
