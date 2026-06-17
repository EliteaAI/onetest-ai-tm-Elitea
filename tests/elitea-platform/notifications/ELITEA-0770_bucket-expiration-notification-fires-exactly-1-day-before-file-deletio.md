---
id: ELITEA-0770
title: "Bucket Expiration Notification Fires Exactly 1 Day Before File Deletion Begins"
priority: critical
type: functional
module: notifications
status: ready
execution_type: manual
tags: [feat:notifications, user_story:3414, feat:artifacts, r-2.0.2]
requirements: [ProjectAlita/projectalita.github.io#3414]
---
# ELITEA-0770: Bucket Expiration Notification Fires Exactly 1 Day Before File Deletion Begins

**Module:** Notifications · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the system sends exactly one notification per bucket, 1 day before file deletion begins — and that when retention is set to 1 day, the notification fires immediately on creation (since 1 day before = creation time).

**Coverage:**
- Exactly 1 notification per bucket (1 day before deletion, no earlier)
- Special case: Days=1 retention → notification fires immediately on creation
- No notification fires on creation for retention > 1 day
- Notification message states: files will start being deleted in 24 hours, the bucket itself will remain
- Notification scoped to bucket creator only
- AC1 (timing), AC3 (message content) from issue EliteaAI/elitea_issues#3414

## Preconditions

- Logged in to {{base_url}} as the bucket creator
- Test environment supports date-offset simulation to advance to 1 day before deletion
- Browser: Chrome (latest)

## Test Data

| Bucket Name | Retention Type | Value | Expected notification trigger |
|---|---|---|---|
| `notif-days-1` | Days | 1 | Immediately on creation (1 day before = creation time) |
| `notif-days-2` | Days | 2 | 1 day before day 2 expiry (date simulation needed) |
| `notif-weeks-1` | Weeks | 1 | 1 day before week 1 expiry (date simulation needed) |

Expected message format:
"Bucket retention notice (1 day left)
Your bucket {bucket_name} will start deleting files in 24 hours according to its retention policy (files are removed based on each file's creation date; the bucket itself will remain)."

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Artifacts. Create bucket `notif-days-1` with retention: Days, Value: 1. Click Save. | Bucket created. An immediate notification for `notif-days-1` appears in the Notification Center (since 1 day before deletion = creation time). |
| 2 | Open the Notification Center (bell icon). Read the full notification message for `notif-days-1`. | Exactly 1 notification for `notif-days-1` is present. Message states: 'Bucket retention notice (1 day left) — Your bucket notif-days-1 will start deleting files in 24 hours according to its retention policy (files are removed based on each file's creation date; the bucket itself will remain).' Bucket name is a clickable link. |
| 3 | Navigate to Artifacts. Create bucket `notif-days-2` with retention: Days, Value: 2. Click Save. | Bucket created. No notification appears immediately for `notif-days-2` (notification triggers 1 day before deletion, not on creation). |
| 4 | Open the Notification Center. Scan for any entry referencing `notif-days-2`. | No notification for `notif-days-2` is present at creation time. |
| 5 | Skip 1 day OR Using date-offset simulation, advance the environment date to 1 day before `notif-days-2` expiry. Open the Notification Center. | Exactly 1 notification for `notif-days-2` appears with the same message format, referencing 24 hours until file deletion and that the bucket will remain. |
| 6 | Count all notification entries for `notif-days-2`. | Exactly 1 entry — no duplicates. |
| 7 | Create bucket `notif-weeks-1` with retention: Weeks, Value: 1. Open the Notification Center immediately. | No notification for `notif-weeks-1` appears on creation. |
| 8 | Skip 6 days OR Using date simulation, advance to 1 day before the Weeks expiry of `notif-weeks-1`. Open the Notification Center. | Exactly 1 notification for `notif-weeks-1` appears with the same message format. |

## Expected Final State

Exactly 1 notification for `notif-weeks-1` appears with the same message format.

## Pass/Fail Criteria

**Pass:**
- Days=1 bucket: notification fires immediately on creation
- Days>1 and Weeks buckets: no notification on creation; exactly 1 notification fires 1 day before deletion
- Message explicitly states: files deleted in 24 hours, bucket itself remains, files removed based on creation date
- Bucket name in notification is a clickable hyperlink
- No duplicate notifications for any bucket

**Fail:**
- Days=1 bucket: no immediate notification appears
- Days=2 or Weeks bucket: notification fires on creation (before the 1-day threshold)
- More than 1 notification exists for the same bucket
- Message omits that the bucket itself will remain or omits file creation date as deletion basis
