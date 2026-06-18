---
id: ELITEA-0751
title: "Navigation from Notification Action Link Opens Correct Page"
priority: high
type: functional
module: notifications
status: ready
execution_type: manual
tags: [feat:notifications, feat:tokens, issue:3287, r-2.0.2]
requirements: [EliteaAI/elitea_issues#3287]
---
# ELITEA-0751: Navigation from Notification Action Link Opens Correct Page

**Module:** Notifications · **Priority:** High · **Type:** Functional

**Objective:** Verify that clicking the "Manage Personal Access Tokens" action link in the notification navigates the user to Private project → Personal Access Tokens page.

## Preconditions

- User is authenticated and has access to Private project → Personal Access Tokens
- A Personal Access Token expiration notification is present in Notification Center

## Test Data

- Token name: "Link Navigation Test Token"
- Expiration configured: 3 days

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Create a Personal Access Token "Link Navigation Test Token" with 3-day expiration |  |
| 2 | Wait until T+48h (24 hours before expiration) |  |
| 3 | Open Notification Center and verify the notification is present |  |
| 4 | Click the "Manage Personal Access Tokens" action link in the notification |  |
| 5 | Verify the browser navigates to the correct page |  |
| 6 | Verify the URL is: `{{base_url}}` (or equivalent environment URL) |  |
| 7 | Verify the Personal Access Tokens page loads successfully |  |
| 8 | Verify the token "Link Navigation Test Token" is visible in the tokens list |  |

## Expected Final State

- Clicking the action link navigates to Private project → Personal Access Tokens page
- The correct URL is loaded
- The page displays the user's Personal Access Tokens list
- The token that triggered the notification is visible in the list

## Pass/Fail Criteria

**Pass:** All steps complete as expected.

**Fail:** Any step produces an unexpected result or error.
