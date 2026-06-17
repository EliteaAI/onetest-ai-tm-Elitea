---
id: ELITEA-0501
title: "Chat UI Elements - Model, Tools, Participants"
priority: medium
type: functional
module: chat-interface
status: ready
execution_type: automated
automation_test_id:
  - test_chat_interface.py:TestConversationUIElements.test_model_selector_functional
test_chat_interface.py:TestConversationUIElements.test_internal_tools_toggle
test_chat_interface.py:TestHashSearch.test_hash_search_participants
test_chat_interface.py:TestHashSearch.test_add_participant_via_hash_search
tags: []
requirements: []
---
# ELITEA-0501: Chat UI Elements - Model, Tools, Participants

**Module:** Chat Interface · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that model selector allows switching AI models, internal tools can be toggled, and # search works for adding participants to conversations.

## Preconditions

- User logged into Elitea
- Multiple AI models configured
- Other users/agents available

## Test Data

- URL: {{base_url}}
- Models: Claude 4.5, GPT-5, etc.

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| ? | Click model selector dropdown | List of available models shown |
| ? | Select different model | Model switches, reflected in UI |
| ? | Toggle internal tools | Toggle state changes |
| ? | Type # in chat input | Search dropdown appears with participants |
| ? | Select participant from # search | Participant added to conversation |

## Expected Final State

Participant added to conversation

## Pass/Fail Criteria

**Pass:**
- Model selector shows available models
- Model switch works
- Tools toggle changes state
- # search finds participants
- Participant added successfully

**Fail:**
- Models don't load
- Switch doesn't persist
- Toggle broken
- Search returns no results
- Add participant fails
