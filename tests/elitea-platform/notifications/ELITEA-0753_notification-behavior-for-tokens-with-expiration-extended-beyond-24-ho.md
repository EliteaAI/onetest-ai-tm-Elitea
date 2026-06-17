---
id: ELITEA-0753
title: "Notification Behavior for Tokens with Expiration Extended Beyond 24 Hours"
priority: medium
type: functional
module: notifications
status: ready
execution_type: manual
tags: [feat:notifications, feat:tokens, issue:3287, r-2.0.2]
requirements: [EliteaAI/elitea_issues#3287]
---
# ELITEA-0753: Notification Behavior for Tokens with Expiration Extended Beyond 24 Hours

**Module:** Notifications · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the notification behavior when a token's expiration is extended AFTER a 24-hour expiration notification has already been sent — ensuring no duplicate notifications are created for the same token.

## Preconditions

- User is authenticated and has access to Private project → Personal Access Tokens
- A Personal Access Token "Extension Test Token" with 2-day expiration exists
- The token has already triggered a 24-hour expiration notification

## Test Data

- Token name: "Extension Test Token"
- Initial expiration: 2 days from creation
- Current time: T+24h (notification already sent)
- Extension action: Extend expiration by +3 days (new total: 5 days from creation)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Create a Personal Access Token "Extension Test Token" with 2-day expiration |  |
| 2 | Wait until T+24h (24 hours before initial expiration) — notification is sent |  |
| 3 | Open Notification Center and verify the notification is present |  |
| 4 | Navigate to Private project → Personal Access Tokens page |  |
| 5 | Extend the expiration of "Extension Test Token" by +3 days (new expiration: 5 days from creation) |  |
| 6 | Wait until the new 24-hour notification trigger point (T+24h + 72h = T+96h) |  |
| 7 | Open Notification Center |  |
| 8 | Verify that NO duplicate notification has been created |  |
| 9 | Verify that only the original notification remains (or has been cleared if the extension logic clears stale notifications) |  |

## Expected Final State

- Original notification sent at T+24h
- After expiration extension, NO duplicate notification is created
- The notification system respects the "one notification per token" rule
- Notification either remains as-is or is cleared after extension (behavior to be confirmed during implementation)

## Pass/Fail Criteria

**Pass:** All steps complete as expected.

**Fail:** Any step produces an unexpected result or error.
