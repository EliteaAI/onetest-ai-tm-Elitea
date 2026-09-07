---
id: ELITEA-3215
title: "Folder operation failure shows a standard error notification and preserves prior state"
priority: medium
type: functional
module: social-folders
status: draft
execution_type: manual
tags: [feat:social-folders, issue:5194, error-handling]
requirements: [EliteaAI/elitea_issues#5194]
---
# ELITEA-3215: Folder Operation Failure Handling

**Module:** Social Folders · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that a failed folder operation (create, rename, move, remove, or delete) shows a standard error notification without a success toast, leaves state unchanged from baseline once connectivity is restored, and that retrying without failure completes normally.

## Entities to Test

Execute this case independently for each entity type below, using fresh disposable test data per entity. Do not share data or results between rows.

- [ ] Agents
- [ ] Skills
- [ ] Pipelines
- [ ] Toolkits & Indexes
- [ ] MCPs
- [ ] Credentials

## Preconditions

- A disposable folder and at least one disposable/recoverable entity are available.
- A method to simulate a network/server failure is available (e.g., browser devtools offline mode or blocking the relevant request) for exactly one folder operation (create, rename, move, remove, or delete).
- Record the baseline state (folder existence, count, entity assignment) before the failure simulation.

## Steps

| # | Action | Expected Result |
|---|---|---|
| 1 | Simulate a network/server failure and attempt one folder operation. | The operation does not complete. |
| 2 | Inspect the notification shown. | A standard error notification is shown; no success toast appears. |
| 3 | Restore connectivity and inspect state. | State matches the recorded baseline with no partial change. |
| 4 | Retry the same operation without simulating failure. | The operation completes normally, confirming this is not a persistent defect. |

## Expected Final State

After restoring connectivity, no partial or inconsistent state remains from the failed attempt; the retried operation completes successfully.

## Pass/Fail Criteria

**Pass:**
- The failed operation does not complete and shows a standard error notification with no success toast.
- State matches baseline after restoring connectivity, with no partial change.
- Retrying without failure completes the operation normally.

**Fail:**
- The operation appears to complete despite the failure, or a success toast is shown.
- State diverges from baseline (partial change) after restoring connectivity.
- The retried operation still fails, indicating a persistent defect rather than a transient failure.

## Cleanup

Delete the disposable folder and confirm the entity remains available and unfiled.
