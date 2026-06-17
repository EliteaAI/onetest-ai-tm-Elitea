---
id: ELITEA-0755
title: "No Notification Sent for Tokens with Total Expiration Duration ≤ 24 Hours"
priority: high
type: functional
module: notifications
status: ready
execution_type: manual
tags: [feat:notifications, feat:tokens, issue:3287, r-2.0.2]
requirements: [EliteaAI/elitea_issues#3287]
---
# ELITEA-0755: No Notification Sent for Tokens with Total Expiration Duration ≤ 24 Hours

**Module:** Notifications · **Priority:** High · **Type:** Functional

**Objective:** Verify that Personal Access Tokens with a total lifetime of 24 hours or less do NOT trigger any expiration notifications, regardless of the configuration unit used (hours, minutes, or exactly 1 day).

**Preconditions:**
- User is authenticated and has access to Private project → Personal Access Tokens
- Notification Center is accessible

**Test Data:**

| Token Name | Expiration Config | Total Duration | Expected Notification |
|------------|-------------------|----------------|----------------------|
| Token 12h | 12 hours | 12 hours (< 24h) | No notification |
| Token 1h | 1 hour | 1 hour (< 24h) | No notification |
| Token 30m | 30 minutes | 30 minutes (< 24h) | No notification |
| Token 1d | 1 day | 24 hours (= 24h) | No notification |
| Token 25h | 25 hours | 25 hours (> 24h) | Notification sent at T+1h |
| Token 2d | 2 days | 48 hours (> 24h) | Notification sent at T+24h |

**Steps:**
1. Create all 6 tokens listed in the test data table with their respective expiration configurations
2. Wait until each token reaches the notification trigger point (if applicable)
3. For tokens with duration ≤ 24h: verify NO notification appears in Notification Center at any time before expiration
4. For tokens with duration > 24h: verify notification IS sent exactly 24 hours before expiration
5. Check Notification Center after all tokens have expired to confirm no late notifications were generated

**Expected Result:**
- Tokens with total lifetime ≤ 24 hours (12h, 1h, 30m, exactly 1 day) produce ZERO notifications
- Tokens with total lifetime > 24 hours (25h, 2d) produce exactly one notification 24 hours before expiration
- The exclusion rule is duration-based, not configuration-unit-based
- No notifications appear for excluded tokens at any point during or after their lifetime

## Preconditions

- Logged in to ELITEA (`{{base_url}}`)

## Expected Final State

Verify that Personal Access Tokens with a total lifetime of 24 hours or less do NOT trigger any expiration notifications, regardless of the configuration unit used (hours, minutes, or exactly 1 day).

## Pass/Fail Criteria

**Pass:** All steps complete as expected.

**Fail:** Any step produces an unexpected result or error.
