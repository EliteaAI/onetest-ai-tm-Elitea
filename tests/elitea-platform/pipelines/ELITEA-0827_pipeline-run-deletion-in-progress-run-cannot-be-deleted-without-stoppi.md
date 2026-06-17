---
id: ELITEA-0827
title: "Pipeline Run Deletion — In-Progress Run Cannot Be Deleted Without Stopping First"
priority: high
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [feat:pipelines, story:2186]
requirements: [ProjectAlita/projectalita.github.io#2186]
---
# ELITEA-0827: Pipeline Run Deletion — In-Progress Run Cannot Be Deleted Without Stopping First

**Module:** Pipelines · **Priority:** High · **Type:** Functional

**Objective:** Verify that a run currently In Progress cannot be deleted directly — the user must stop it first — and that deletion becomes available after the run is stopped.

**Coverage:**
- Delete icon hidden or disabled for In Progress runs
- Attempt to delete an In Progress run is blocked with appropriate feedback
- After manual stop, delete icon becomes enabled/available
- Stopped run can then be deleted successfully

## Preconditions

- Logged in at {URL}, project {Project} selected
- User has pipelines.execute, pipelines.delete, pipelines.stop permissions
- Pipeline "Test Pipeline — Deletion Block" created: LLM node (System: "You must create story", Task: "Create some interesting long story"), set as entrypoint, saved
- Pipeline open on Configuration tab → Flow View

## Test Data

- Pipeline name: "Test Pipeline — Deletion Block"
- Chat input: "run"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Type "run" in chat input. Press Enter. Immediately observe the run chipset. | Blue loading icon displayed. Run is In Progress. |
| 2 | Look for a Delete icon on the In Progress chipset. | Delete icon is either absent or visibly disabled/grayed out. |
| 3 | If Delete icon appears clickable, attempt to click it. | Delete is blocked. An error or warning message appears stating the run must be stopped first — OR the action is silently prevented with no deletion occurring. |
| 4 | Click the Stop button on the running chipset. Confirm if prompted. Wait for stopped state. | Run transitions to Stopped state (orange stop icon). |
| 5 | Look for the Delete icon on the now-stopped chipset. | Delete icon is now visible and enabled/clickable. |
| 6 | Click Delete. Confirm if prompted. | Stopped run is deleted from Flow View. No run chipset remains. |

## Expected Final State

Stopped run is deleted from Flow View. No run chipset remains.

## Pass/Fail Criteria

**Pass:**
- In-progress runs are protected from direct deletion
- Clear user feedback when deletion attempt is blocked
- Delete icon becomes available after stop
- Stopped run deletes successfully

**Fail:**
- In-progress run can be deleted without stopping first
- No feedback when deletion attempt is blocked
- Delete icon remains disabled even after run stops
- Deletion of stopped run fails
