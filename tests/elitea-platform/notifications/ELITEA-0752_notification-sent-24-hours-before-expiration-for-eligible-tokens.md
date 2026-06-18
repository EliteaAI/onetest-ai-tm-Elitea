---
id: ELITEA-0752
title: "Notification Sent 24 Hours Before Expiration for Eligible Tokens"
priority: critical
type: functional
module: notifications
status: ready
execution_type: manual
tags: [feat:notifications, feat:tokens, issue:3287, r-2.0.2]
requirements: [EliteaAI/elitea_issues#3287]
---
# ELITEA-0752: Notification Sent 24 Hours Before Expiration for Eligible Tokens

**Module:** Notifications · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that when a Personal Access Token with expiration duration > 24 hours reaches exactly 24 hours before expiration, the notification system sends exactly one in-app notification to the token owner.

## Preconditions

- User is authenticated and has access to Private project → Personal Access Tokens
- Notification Center is accessible

## Test Data

- Token name: "API Integration Token"
- Expiration configured: 3 days from creation
- Current time: T+48h (exactly 24 hours before expiration)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Private project → Personal Access Tokens page |  |
| 2 | Create a new Personal Access Token with name "API Integration Token" and expiration set to 3 days |  |
| 3 | Wait until the token reaches exactly 24 hours before expiration (T+48h) |  |
| 4 | Open the Notification Center |  |
| 5 | Verify the notification is present with: - Title: "Personal access token expires in 1 day" - Body: "Your personal access token API Integration Token will expire in 24 hours. After expiration, it will no longer work. You can delete and recreate a new token if needed." - Action link: "Manage Personal Access Tokens" |  |
| 6 | Verify the notification appears only once (no duplicates) |  |

## Expected Final State

- Exactly one notification is sent to the token owner at T+48h (24 hours before expiration)
- Notification contains the correct title, body, token name, and action link
- Notification is visible in the Notification Center
- No duplicate notifications are created

## Pass/Fail Criteria

**Pass:** All steps complete as expected.

**Fail:** Any step produces an unexpected result or error.
