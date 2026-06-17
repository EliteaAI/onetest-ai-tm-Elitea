---
id: ELITEA-0756
title: "Notification Scoped to Token Owner Only"
priority: critical
type: functional
module: notifications
status: ready
execution_type: manual
tags: [feat:notifications, feat:tokens, issue:3287, r-2.0.2]
requirements: [EliteaAI/elitea_issues#3287]
---
# ELITEA-0756: Notification Scoped to Token Owner Only

**Module:** Notifications · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that Personal Access Token expiration notifications are delivered only to the user who created the token, and not to other users in the same project or platform administrators.

**Preconditions:**
- Two users exist: User A (token owner) and User B (non-owner)
- Both users have access to the same Private project
- User A has created a Personal Access Token "Owner Scoped Token" with 2-day expiration

**Test Data:**
- User A: Token owner
- User B: Non-owner user in the same project
- Token name: "Owner Scoped Token"
- Expiration configured: 2 days

**Steps:**
1. User A creates a Personal Access Token "Owner Scoped Token" with 2-day expiration
2. Wait until T+24h (24 hours before expiration)
3. User A opens Notification Center and verifies the notification is present
4. User B logs in with their account
5. User B navigates to Notification Center
6. Verify that User B does NOT see the notification for "Owner Scoped Token"
7. Verify that User B's Notification Center does not show any notifications related to User A's tokens

**Expected Result:**
- Notification is visible only to User A (token owner)
- User B does not receive or see the notification
- Notification scoping is strictly enforced per token owner

## Preconditions

- Logged in to ELITEA (`{{base_url}}`)

## Expected Final State

Verify that Personal Access Token expiration notifications are delivered only to the user who created the token, and not to other users in the same project or platform administrators.

## Pass/Fail Criteria

**Pass:** All steps complete as expected.

**Fail:** Any step produces an unexpected result or error.
