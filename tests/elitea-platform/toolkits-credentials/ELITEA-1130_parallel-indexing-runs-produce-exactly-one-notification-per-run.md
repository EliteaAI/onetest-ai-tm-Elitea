---
id: ELITEA-1130
title: "Parallel Indexing Runs Produce Exactly One Notification Per Run"
priority: medium
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [feat:notifications, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3716]
---
# ELITEA-1130: Parallel Indexing Runs Produce Exactly One Notification Per Run

**Module:** Toolkits Credentials · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that when multiple indexing runs are triggered simultaneously (in parallel) across different indexes or toolkits, each run produces exactly one failure notification in the Notifications panel — with no duplicate notifications and no cross-run contamination.

## Preconditions

- A project exists and the user has Editor role or higher.
- At least 2 toolkits (or 2 indexes within one toolkit) with invalid credentials exist, so all parallel runs will fail.
- The Notifications panel is empty at the start of the test (no pre-existing notifications).

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the first toolkit (or first index in the Indexes tab) and click the Index / Run button to start indexing. Do NOT wait for it to complete — immediately proceed to the next step. | First indexing run starts and is in progress. |
| 2 | Without waiting for the first run to finish, open the second toolkit (or second index) in a new browser tab or via navigation, and click the Index / Run button to start its indexing run concurrently. | Second indexing run starts while the first run is still in progress. Both runs are executing simultaneously. |
| 3 | Optionally trigger a third indexing run on a third toolkit or index in the same manner — before either of the previous runs complete. | Third indexing run starts. All triggered runs are executing in parallel. |
| 4 | Wait for all parallel indexing runs to complete (reach a failure state). | All parallel runs complete with failure status. Each index/toolkit shows a failed state. |
| 5 | Click the bell-icon in the top navigation bar to open the Notifications panel. | Notifications panel opens and displays all failure notifications. |
| 6 | Count the total number of failure notifications in the panel and verify they correspond 1-to-1 with the triggered runs. | Total notification count equals the number of parallel runs triggered (e.g., 2 runs → 2 notifications, 3 runs → 3 notifications). No run has produced a duplicate notification. Each notification references a distinct index name. |

## Expected Final State

Total notification count equals the number of parallel runs triggered (e.g., 2 runs → 2 notifications, 3 runs → 3 notifications). No run has produced a duplicate notification. Each notification references a distinct index name.

## Pass/Fail Criteria

- Notification count exactly equals the number of parallel runs triggered.
- No single run produces more than 1 notification (no duplicates).
- Each notification references a distinct index/toolkit name.
- No cross-run contamination (notifications of one run do not appear duplicated due to another run).
- All notifications have red icons indicating failure.
