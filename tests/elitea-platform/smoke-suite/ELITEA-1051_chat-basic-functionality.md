---
id: ELITEA-1051
title: "Chat Basic Functionality"
priority: critical
type: functional
module: smoke-suite
status: ready
execution_type: automated
automation_test_id:
  - tests.ui.chat.test_chat_interface.test_chat_page_loads_with_functional_input
  - tests.ui.chat.test_chat_interface.test_chat_page_loads_successfully
  - tests.ui.chat.test_chat_interface.test_message_input_is_functional
  - tests.ui.chat.test_chat_interface.test_chat_message_history_displays
tags: []
requirements: []
---
# ELITEA-1051: Chat Basic Functionality

**Module:** Smoke Suite · **Priority:** Critical · **Type:** Functional

**Objective:** Verify basic chat interface functionality: UI elements load correctly, user can send messages, and AI responds successfully.

## Preconditions

- User is logged in
- Valid API token configured in .env.test
- Active conversation exists or can be created
- AI model (Claude 4.5 Sonnet) is available

## Test Data

- URL: {{base_url}}
- Test user: alita@elitea.ai
- Password: rokziJ-nuvzo4-hucmih
- Test message: "Hello, this is a test message"
- AI model: Claude 4.5 Sonnet (default)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| ? | Navigate to Chat page (from main menu or direct URL /chat) | Chat page loads within 3 seconds |
| ? | Verify chat interface elements are present and functional: message input textarea, Send button, Attach files button, Sidebar toggle | All UI elements visible: textarea is editable, buttons are clickable |
| ? | Type a simple test message in the message input: 'Hello, this is a test message' | Text appears in the input field without errors |
| ? | Click the Send button (or press Enter) | Message is sent, user message appears in chat history immediately |
| ? | Wait for AI response (max 30 seconds) | AI responds within 30 seconds, response appears below user message |
| ? | Verify chat history displays both messages in correct order (user message first, then AI response) | Both messages visible in chat history, correct chronological order |
| ? | Verify no console errors or failed network requests | No errors in browser console, all API calls successful (check Network tab) |

## Expected Final State

No errors in browser console, all API calls successful (check Network tab)

## Pass/Fail Criteria

**Pass:**
- All 7 test steps pass
- AI response time < 30 seconds
- No console errors or failed network requests
- Both messages visible in chat history

**Fail:**
- Chat page fails to load
- Message input not functional
- AI does not respond within 30 seconds
- Network errors in console
- Messages not displayed correctly
