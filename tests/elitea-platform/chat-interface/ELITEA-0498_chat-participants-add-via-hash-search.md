---
id: ELITEA-0498
title: "Chat Participants - Add via Hash Search"
priority: medium
type: functional
module: chat-interface
status: ready
execution_type: automated
automation_test_id:
  - test_chat_interface.py:TestHashSearch.test_add_participant_via_hash_search
tags: []
requirements: []
---
# ELITEA-0498: Chat Participants - Add via Hash Search

**Module:** Chat Interface · **Priority:** Medium · **Type:** Functional

**Objective:** Verify adding participants to conversation via # search and selection.

**Coverage:**
- Type # in message input to trigger participant search
- Search results display available participants
- Click participant to add to conversation

## Preconditions

- User is logged in to {{base_url}} via Keycloak
- At least one conversation exists (create one manually if needed)
- At least one agent exists in the system (for participant search results)
- Browser: Chrome or Chromium
- Note: This feature may not be available on the staging environment

## Test Data

- URL: {{base_url}}
- Search trigger: type '#' character in the message input
- Test search queries: #agent, #test

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chat and open an existing conversation. Wait for the page to fully load and the message input field to be visible. | The chat page is loaded. The message input field is editable. |
| 2 | Click on the message input field and type '#agent'. | Typing the '#' character triggers a participant search dropdown. |
| 3 | Check if a dropdown/popup appears with a list of searchable participants (agents, users, etc.). | A dropdown is visible within 5 seconds showing participant options. If no dropdown appears, this feature may be disabled on the current environment. |
| 4 | If the dropdown appeared, click on the first option to add the participant to the conversation. | The participant is added to the conversation. The dropdown closes. |

## Expected Final State

The participant is added to the conversation. The dropdown closes.

## Pass/Fail Criteria

**Pass:**
- Hash character triggers participant search
- Dropdown appears with participant results
- Clicking participant adds them to conversation
- Feature correctly skips if not available on stage

**Fail:**
- Hash character does nothing (no dropdown)
- Dropdown appears but is empty
- Clicking participant causes error
- Note: Test may skip if hash_search feature is disabled on stage
