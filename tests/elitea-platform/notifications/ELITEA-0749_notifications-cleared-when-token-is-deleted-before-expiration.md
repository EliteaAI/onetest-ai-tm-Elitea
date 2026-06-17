---
id: ELITEA-0749
title: "Notifications Cleared When Token is Deleted Before Expiration"
priority: medium
type: functional
module: notifications
status: ready
execution_type: manual
tags: [feat:notifications, feat:tokens, issue:3287, r-2.0.2]
requirements: [EliteaAI/elitea_issues#3287]
---
# ELITEA-0749: Notifications Cleared When Token is Deleted Before Expiration

**Module:** Notifications · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that when a user deletes a Personal Access Token that has an active expiration notification (before the token actually expires), the corresponding notification is automatically removed from the Notification Center.

**Preconditions:**
- User is authenticated and has access to Private project → Personal Access Tokens
- A Personal Access Token "Delete Before Expiration Token" with 3-day expiration exists
- The token has already triggered a 24-hour expiration notification

**Test Data:**
- Token name: "Delete Before Expiration Token"
- Expiration configured: 3 days
- Current time: T+48h (notification already sent)

**Steps:**
1. Create a Personal Access Token "Delete Before Expiration Token" with 3-day expiration
2. Wait until T+48h (24 hours before expiration) — notification is sent
3. Open Notification Center and verify the notification is present
4. Navigate to Private project → Personal Access Tokens page
5. Delete the token "Delete Before Expiration Token"
6. Navigate back to Notification Center
7. Verify the notification for "Delete Before Expiration Token" is NO LONGER present
8. Refresh the page and verify the notification remains absent

**Expected Result:**
- Notification is present before token deletion
- Notification is automatically removed from Notification Center after token deletion
- Notification does not reappear after page refresh or logout/login
- Notification lifecycle is tied to token existence

## Preconditions

- Logged in to ELITEA (`{{base_url}}`)

## Expected Final State

Verify that when a user deletes a Personal Access Token that has an active expiration notification (before the token actually expires), the corresponding notification is automatically removed from the Notification Center.

## Pass/Fail Criteria

**Pass:** All steps complete as expected.

**Fail:** Any step produces an unexpected result or error.
