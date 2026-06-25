---
id: ELITEA-1341
title: "Voice Mini Player Not Visible by Default in Chat (Regression #5235)"
priority: high
type: functional
module: voice
status: ready
execution_type: automated
automation_test_id:
  - test_voice_configuration.py:test_voice_settings_not_visible_by_default
tags: []
requirements: []
---
# ELITEA-1341: Voice Mini Player Not Visible by Default in Chat (Regression #5235)

**Module:** Voice · **Priority:** High · **Type:** Functional

**Objective:** Verify that the Voice Mini Player / Read-out controls are NOT visible in a default chat conversation before the Voice or Read-out feature has been explicitly activated. Regression test for Bug #5235.

**Coverage:**
- After receiving an AI response in a new conversation, Voice Mini Player must not be visible
- Voice settings controls should only appear when Read-out or Voice mode is explicitly enabled by the user

## Preconditions

- User is logged in to {{base_url}} via Keycloak
- Browser: Chrome or Chromium
- AI model is available for generating responses
- No Voice / Read-out feature has been activated in the current session

## Test Data

- URL: {{base_url}}
- Test message: `hi`
- Bug reference: https://github.com/EliteaAI/elitea_issues/issues/5235

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chat (sidebar). Click 'Create Conversation' to start a fresh conversation. | A new conversation opens with no messages. |
| 2 | Type `hi` in the message input and press Enter. Wait for AI response (up to 30 seconds). | AI responds. Both the user message and AI response are visible in the chat history. |
| 3 | After the AI response appears, inspect the chat area for any Voice Mini Player or Read-out controls (audio player, play/pause button, voice waveform, etc.). | Voice Mini Player is NOT visible anywhere in the chat area. No audio controls are rendered by default. |

## Expected Final State

The chat conversation contains user and AI messages, but no Voice Mini Player or Read-out controls are visible — these should only appear when the feature is explicitly activated.

## Pass/Fail Criteria

**Pass:**
- AI responds within 30 seconds
- No Voice Mini Player or Read-out audio controls visible in the default chat state after AI response

**Fail:**
- Voice Mini Player appears in the chat area without the user activating Read-out or Voice mode (regression of Bug #5235)
- Any unexpected audio controls visible by default
