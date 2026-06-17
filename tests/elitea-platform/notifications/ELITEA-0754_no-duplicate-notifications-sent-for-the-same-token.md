---
id: ELITEA-0754
title: "No Duplicate Notifications Sent for the Same Token"
priority: critical
type: functional
module: notifications
status: ready
execution_type: manual
tags: [feat:notifications, feat:tokens, issue:3287, r-2.0.2]
requirements: [EliteaAI/elitea_issues#3287]
---
# ELITEA-0754: No Duplicate Notifications Sent for the Same Token

**Module:** Notifications · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the notification system sends exactly one notification per token, and no duplicate notifications are created even after page refresh, logout/login, or repeated notification center visits.

**Preconditions:**
- User is authenticated and has access to Private project → Personal Access Tokens
- A Personal Access Token has already triggered a 24-hour expiration notification

**Test Data:**
- Token name: "Test Token Duplicate Check"
- Expiration configured: 2 days from creation
- Notification already sent at T+24h

**Steps:**
1. Navigate to Notification Center and verify the existing notification for "Test Token Duplicate Check" is present
2. Refresh the browser page
3. Check Notification Center again — verify only one notification exists
4. Log out and log back in
5. Navigate to Notification Center — verify only one notification exists
6. Wait 1 hour (T+25h) and check Notification Center again
7. Verify no additional notifications have been created

**Expected Result:**
- Exactly one notification exists for the token throughout all steps
- No duplicate notifications are created after page refresh, logout/login, or time passage
- The notification remains singular and persistent

## Preconditions

- Logged in to ELITEA (`{{base_url}}`)

## Expected Final State

Verify that the notification system sends exactly one notification per token, and no duplicate notifications are created even after page refresh, logout/login, or repeated notification center visits.

## Pass/Fail Criteria

**Pass:** All steps complete as expected.

**Fail:** Any step produces an unexpected result or error.
