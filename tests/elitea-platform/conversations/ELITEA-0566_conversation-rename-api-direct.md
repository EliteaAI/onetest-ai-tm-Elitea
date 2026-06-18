---
id: ELITEA-0566
title: "Conversation Rename - API Direct"
priority: medium
type: functional
module: conversations
status: ready
execution_type: automated
automation_test_id:
  - test_conversation_management.py:TestConversationActions.test_conversation_api_rename
tags: []
requirements: []
---
# ELITEA-0566: Conversation Rename - API Direct

**Module:** Conversations · **Priority:** Medium · **Type:** Functional

**Objective:** Verify conversation rename via direct API call.

**Coverage:**
- API endpoint to rename conversation
- Conversation name updated successfully
- Updated name persists

## Preconditions

- User is logged in to {{base_url}} via Keycloak
- At least one conversation exists (create one manually if needed)
- A REST API testing tool is available (e.g., Postman, curl, or browser dev tools) for the API rename step
- Browser: Chrome or Chromium

## Test Data

- URL: {{base_url}}
- API base URL: {{base_url}}
- New conversation name: at_renamed (must be 3-50 characters)
- Project ID: 23

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chat and open an existing conversation. Note the conversation's current name and ID. | The conversation is open. The current name and ID are known. |
| 2 | Note the original conversation name (visible in the sidebar or URL). | The original name is recorded for comparison. |
| 3 | Using an API tool (Postman, curl, etc.), send a PUT request to rename the conversation to 'at_renamed'. Use the rename endpoint with the conversation ID and body {"name": "at_renamed"}. | The API returns a success response (HTTP 200). The name is updated. |
| 4 | Refresh the Chat page in the browser. Verify the conversation name in the sidebar now shows 'at_renamed'. | The conversation name is displayed as 'at_renamed' in the sidebar. The rename persisted. |

## Expected Final State

The conversation name is displayed as 'at_renamed' in the sidebar. The rename persisted.

## Pass/Fail Criteria

**Pass:**
- Rename API call returns 200
- Conversation name updated to "at_renamed"
- Name persists on subsequent GET call
- Name meets 3-50 character validation

**Fail:**
- Rename API returns error (404 if wrong path, 400 if invalid name)
- Name not updated after PUT call
- GET returns old name after rename
- API rejects name shorter than 3 or longer than 50 chars
