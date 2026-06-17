---
id: ELITEA-0411
title: "/` Autosuggest Triggered Only When Toolkit or MCP Is in Participants"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [user_story:2925, feat:chat, r-2.0.3]
requirements: [EliteaAI/elitea_issues#2925]
---
# ELITEA-0411: /` Autosuggest Triggered Only When Toolkit or MCP Is in Participants

**Module:** Chat Interface · **Priority:** High · **Type:** Functional

**Objective:** Verify that typing `/` in the chat input triggers an autosuggest dropdown only when at least one Toolkit or MCP has been added to Participants — and produces no dropdown in an empty-Participants conversation.

**Coverage:**
- `/` with toolkit in Participants → autosuggest dropdown appears
- `/` with no toolkits/MCPs in Participants → no dropdown appears

## Preconditions

- Logged in to {{base_url}} as a standard user
- Artifacts toolkit exists and is properly configured
- Conversation A: Artifacts added to Participants
- Conversation B: No toolkits/MCPs added

## Test Data

- Conversation A: Artifacts toolkit in Participants
- Conversation B: empty Participants
- Input text: /

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Conversation A (Artifacts in Participants). Click the chat input box. | Chat input is focused. |
| 2 | Type /. | Autosuggest dropdown appears showing at least Artifacts. |
| 3 | Open Conversation B (empty Participants). Click the chat input box. | Chat input is focused. |
| 4 | Type /. | No autosuggest dropdown appears. The / character appears as plain text. |

## Expected Final State

No autosuggest dropdown appears. The / character appears as plain text.

## Pass/Fail Criteria

**Pass:**
- Dropdown appears in Conversation A after typing /
- No dropdown appears in Conversation B after typing /

**Fail:**
- No dropdown appears even with a configured toolkit in Participants
- Dropdown appears in empty-Participants conversation
