---
id: ELITEA-1135
title: "Scheduled Indexing Failure Produces Exactly One Notification Marked \"by schedule\""
priority: medium
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [feat:notifications, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3716]
---
# ELITEA-1135: Scheduled Indexing Failure Produces Exactly One Notification Marked "by schedule"

**Module:** Toolkits Credentials · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that when a scheduled indexing run fails due to invalid credentials, exactly one failure notification appears in the Notifications panel and it is correctly marked as "by schedule".

## Preconditions

- A project exists and the user has Editor role or higher.
- A toolkit with a configured indexing schedule exists (e.g., set to trigger every few minutes for test purposes).
- The toolkit credential is invalid so that the scheduled run will fail.
- The Notifications panel is empty at the start of the test (or pre-existing notifications are noted).

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the toolkit settings and verify a schedule is configured and active. | Indexing schedule is confirmed as active (e.g., runs every N minutes). |
| 2 | Wait for the scheduled indexing cycle to trigger automatically and complete. | Scheduled indexing run executes and fails due to invalid credentials. |
| 3 | Click the bell-icon in the top navigation bar to open the Notifications panel. | Notifications panel opens and displays notifications. |
| 4 | Count the number of failure notifications produced by the scheduled run. | Exactly ONE failure notification is displayed. No duplicate notification for the same scheduled run exists. |
| 5 | Inspect the notification message and any schedule indicator text. | The notification includes 'by schedule' in its text (e.g., 'Index {name} is failed. by schedule') and has a red icon. |

## Expected Final State

The notification includes 'by schedule' in its text (e.g., 'Index {name} is failed. by schedule') and has a red icon.

## Pass/Fail Criteria

- Notifications panel shows exactly 1 failure notification for the scheduled run.
- No duplicate notification exists.
- Notification message contains 'by schedule'.
- Notification has a red icon.
