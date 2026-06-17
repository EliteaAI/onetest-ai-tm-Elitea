---
id: ELITEA-1134
title: "Single Failure Notification — Initial Indexing Failure Triggered from Indexes Tab"
priority: medium
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [feat:notifications, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3716]
---
# ELITEA-1134: Single Failure Notification — Initial Indexing Failure Triggered from Indexes Tab

**Module:** Toolkits Credentials · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that when an indexing operation fails due to invalid credentials and is triggered from the Indexes Tab, exactly one failure notification appears in the Notifications panel — not two duplicates.

## Preconditions

- A project exists and the user has Editor role or higher.
- A toolkit (e.g., Confluence) exists with at least one index configured.
- The toolkit has an invalid credential set.
- No previous indexing notifications are present in the Notifications panel (or the panel is cleared).

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the toolkit (e.g., Confluence) and open the Indexes tab. | Indexes tab is displayed with a list of configured indexes. |
| 2 | Confirm that an invalid credential is assigned to the toolkit. | Invalid credential is in place. |
| 3 | Select an index entry and click the Run button from the Indexes tab. | Indexing starts; a progress indicator or status update appears. |
| 4 | Wait for the indexing operation to complete and reach a failure state. | Indexing fails; failure status is reflected in the UI. |
| 5 | Click the bell-icon in the top navigation bar to open the Notifications panel. | Notifications panel opens and displays notifications. |
| 6 | Count the number of failure notifications related to this indexing operation. | Exactly ONE failure notification is displayed (e.g., 'Index {name} is failed.'). No duplicate notification for the same run exists. |
| 7 | Inspect the notification: check the icon color and message text. | The notification has a red icon and the message references the correct index name. |

## Expected Final State

The notification has a red icon and the message references the correct index name.

## Pass/Fail Criteria

- Notifications panel shows exactly 1 failure notification for the run.
- No identical duplicate notification is visible.
- Notification has a red icon.
- Notification message matches the failed index name.
