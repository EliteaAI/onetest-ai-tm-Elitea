---
id: ELITEA-0828
title: "Pipeline Run Deletion — Remove Completed Runs from Current View and History List"
priority: high
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [feat:pipelines, story:2186]
requirements: [ProjectAlita/projectalita.github.io#2186]
---
# ELITEA-0828: Pipeline Run Deletion — Remove Completed Runs from Current View and History List

**Module:** Pipelines · **Priority:** High · **Type:** Functional

**Objective:** Verify users can delete completed runs from both the current run chipset and the History Icon list, and that deletions persist and correctly affect the history grouping threshold.

**Coverage:**
- Delete icon visible on runs in the history list
- Delete icon visible on the current run chipset
- Deleting from history list removes only that run; others remain
- Deleting the current run promotes the next most recent run as the new current
- History Icon disappears when only 1 run remains after deletion
- Deletion persists after closing and reopening the history list
- Confirmation dialog shown before deletion (if applicable)

## Preconditions

- Logged in at {URL}, project {Project} selected, user has pipelines.delete permission
- Pipeline "Test Pipeline — Run Deletion" created: LLM node (System: "You must create story", Task: "Create some interesting long story"), set as entrypoint, saved
- Pipeline open on Configuration tab → Flow View
- Three completed runs (Run 1, Run 2, Run 3) already executed via chat input before starting test steps

## Test Data

- Pipeline name: "Test Pipeline — Run Deletion"
- Execute 3 runs via chat input "run" before beginning steps

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Verify History Icon visible and Run 3 displayed as current run with green checkmark. | History Icon present. Run 3 chipset shown separately. |
| 2 | Click History Icon. Verify list shows Run 1 and Run 2. | Run 1 and Run 2 listed with their status icons. |
| 3 | Click the Delete icon next to Run 1. Confirm deletion if prompted. | Run 1 removed from history list. Only Run 2 remains in the list. |
| 4 | Close and reopen the history list. | Run 1 still absent. Deletion persisted. Run 2 still present. |
| 5 | Close the history list. Locate the Delete icon on the Run 3 chipset (current run). Click it. Confirm if prompted. | Run 3 chipset removed from Flow View. Run 2 becomes visible as the new current run. |
| 6 | Verify the History Icon state. | History Icon is gone (only 1 run — Run 2 — remains). |

## Expected Final State

History Icon is gone (only 1 run — Run 2 — remains).

## Pass/Fail Criteria

**Pass:**
- Runs deleted immediately from the correct location
- History list updates dynamically after each deletion
- History Icon disappears when ≤1 run remains
- Deletion persists after list reopen
- Deleting current run promotes the next run as current

**Fail:**
- Delete icon missing or non-functional on any location
- Deleted run still appears after list reopen
- Wrong run deleted (other runs affected)
- History Icon remains when ≤1 run exists
- Current run not promoted after deletion of prior current
