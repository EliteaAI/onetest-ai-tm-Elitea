---
id: ELITEA-1340
title: "Context Budget Panel Reflects Profile Max Context Tokens"
priority: high
type: functional
module: chat-interface
status: ready
execution_type: automated
automation_test_id:
  - tests.ui.chat.test_context_management.TestContextManagementSettings.test_context_budget_reflects_profile_max_tokens[10k_tokens]
  - tests.ui.chat.test_context_management.TestContextManagementSettings.test_context_budget_reflects_profile_max_tokens[32k_tokens]
tags: []
requirements: []
---
# ELITEA-1340: Context Budget Panel Reflects Profile Max Context Tokens

**Module:** Chat Interface · **Priority:** High · **Type:** Functional

**Objective:** Verify that the Context Budget panel in chat reflects the Max Context Tokens value configured in the user's profile settings, confirming the setting propagates correctly to new conversations.

**Coverage:**
- User sets Max Context Tokens in profile (e.g. 10,000 tokens)
- User creates a new chat conversation and sends a message
- Context Budget panel appears and displays the configured token limit
- Updated profile value (e.g. 32,000 tokens) also propagates correctly (not cached)

## Preconditions

- User is logged in to {{base_url}} via Keycloak
- Browser: Chrome or Chromium
- AI model is available for generating responses
- Context Management feature is enabled in the platform

## Test Data

- URL: {{base_url}}
- Max Context Tokens variant 1: 10,000
- Max Context Tokens variant 2: 32,000
- Test message: `at_ctx_budget_test_10k` / `at_ctx_budget_test_32k`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to user profile settings (via user avatar or Settings menu). | Profile settings page loads. |
| 2 | Locate the Default Context Management section. Enable context management for new conversations. | The context management toggle is ON. |
| 3 | Set Max Context Tokens to 10,000. Wait for the setting to autosave. Reload the page. | After reload, the Max Context Tokens field shows 10,000 — confirming the value was persisted. |
| 4 | Navigate to Chat (sidebar). Click 'Create Conversation' to start a new conversation. | A fresh conversation opens with no messages. |
| 5 | Type a short test message and send it (press Enter). Wait for AI response (up to 30 seconds). | AI responds. The Context Budget panel becomes visible below the chat input or in the sidebar. |
| 6 | Verify the Context Budget panel is visible and inspect its displayed max token limit. | Context Budget panel shows a max limit equal to 10,000 tokens (matches the profile setting). |
| 7 | Repeat steps 3–6 with Max Context Tokens set to 32,000. | Context Budget panel shows 32,000 tokens — confirming the updated value propagates without stale caching. |

## Expected Final State

Context Budget panel in chat displays the exact Max Context Tokens value configured in the user profile settings for both tested values.

## Pass/Fail Criteria

**Pass:**
- Profile autosaves max_context_tokens (verified by page reload)
- Context Budget panel appears after first message
- Panel displays the exact configured token limit for both 10k and 32k variants
- No stale/cached value from a previous profile setting

**Fail:**
- Context Budget panel does not appear after sending a message
- Panel shows a different token limit than the profile setting
- Profile setting does not persist after page reload
- Feature is entirely absent (skip, not fail, if panel not visible)
