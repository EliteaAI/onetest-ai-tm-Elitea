---
id: ELITEA-1133
title: "Single Failure Notification for Reindexing Failure"
priority: medium
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [feat:notifications, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3716]
---
# ELITEA-1133: Single Failure Notification for Reindexing Failure

**Module:** Toolkits Credentials · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that when a previously successful index is reindexed and fails due to invalid credentials, exactly one failure notification appears in the Notifications panel — not two duplicates.

## Preconditions

- A project exists and the user has Editor role or higher.
- A toolkit has at least one index that was previously indexed successfully.
- The toolkit credential has been changed to an invalid value so that the next indexing run will fail.
- No previous indexing failure notifications are present in the Notifications panel (or the panel is cleared).

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the toolkit and open the Indexes tab. | Indexes tab is displayed; at least one index entry shows a previous successful state. |
| 2 | Select the previously-indexed entry and click the Reindex (or Run) button. | Reindexing starts; a progress indicator or status update appears. |
| 3 | Wait for the reindexing operation to complete and reach a failure state. | Reindexing fails due to invalid credentials; failure status is reflected in the UI. |
| 4 | Click the bell-icon in the top navigation bar to open the Notifications panel. | Notifications panel opens and displays notifications. |
| 5 | Count the number of failure notifications related to this reindexing operation. | Exactly ONE failure notification is displayed (e.g., 'Index {name} is failed.'). No duplicate notification for the same run exists. |
| 6 | Inspect the notification: check the icon color and message text. | The notification has a red icon and the message references the correct index name. |

## Expected Final State

The notification has a red icon and the message references the correct index name.

## Pass/Fail Criteria

- Notifications panel shows exactly 1 failure notification for the reindex run.
- No identical duplicate notification is visible.
- Notification has a red icon.
- Notification message matches the failed index name.
