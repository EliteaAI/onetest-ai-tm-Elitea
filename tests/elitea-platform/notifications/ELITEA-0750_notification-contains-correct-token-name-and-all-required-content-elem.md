---
id: ELITEA-0750
title: "Notification Contains Correct Token Name and All Required Content Elements"
priority: high
type: functional
module: notifications
status: ready
execution_type: manual
tags: [feat:notifications, feat:tokens, issue:3287, r-2.0.2]
requirements: [EliteaAI/elitea_issues#3287]
---
# ELITEA-0750: Notification Contains Correct Token Name and All Required Content Elements

**Module:** Notifications · **Priority:** High · **Type:** Functional

**Objective:** Verify that the Personal Access Token expiration notification displays the correct token name dynamically and contains all required content elements (title, body, token name substitution, action link).

## Preconditions

- User is authenticated and has access to Private project → Personal Access Tokens
- Notification Center is accessible

## Test Data

- Token name variations:
  - "Production API Key"
  - "Test-Token-123"
  - "Token with Special Chars !@#"
  - "Very Long Token Name That Exceeds Normal Length Expectations"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Create a Personal Access Token with name "Production API Key" and 3-day expiration |  |
| 2 | Wait until T+48h (24 hours before expiration) |  |
| 3 | Open Notification Center and verify the notification contains: - **Title:** "Personal access token expires in 1 day" - **Body:** "Your personal access token **Production API Key** will expire in 24 hours. After expiration, it will no longer work. You can delete and recreate a new token if needed." - **Action link text:** "Manage Personal Access Tokens" |  |
| 4 | Repeat steps 1-3 for tokens with names: "Test-Token-123", "Token with Special Chars !@#", and "Very Long Token Name That Exceeds Normal Length Expectations" |  |
| 5 | Verify that each notification correctly substitutes the token name in the body text |  |

## Expected Final State

- Notification title is always "Personal access token expires in 1 day"
- Notification body contains the exact token name (no truncation or escaping issues)
- Token name is dynamically substituted in the placeholder `{token_name}`
- Action link text is "Manage Personal Access Tokens"
- All content elements are present and correctly formatted for all token name variations

## Pass/Fail Criteria

**Pass:** All steps complete as expected.

**Fail:** Any step produces an unexpected result or error.
