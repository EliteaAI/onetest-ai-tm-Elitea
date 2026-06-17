---
id: ELITEA-1200
title: "TC-019 (Jira): Pipeline Using Jira Toolkit Node Executes Successfully After UI Reorganization"
priority: medium
type: functional
module: jira-toolkit-configuration
status: draft
execution_type: manual
tags: [feat:toolkits, issue:4029, int:jira, r-2.0.2]
requirements: [ProjectAlita/projectalita.github.io#4029]
---
# ELITEA-1200: TC-019 (Jira): Pipeline Using Jira Toolkit Node Executes Successfully After UI Reorganization

**Module:** Jira Toolkit Configuration · **Priority:** Medium · **Type:** Functional

**Objective:** Regression test — verify that a Pipeline that uses a Jira Toolkit Node continues to execute successfully after the UI reorganization is deployed. The backend API contract for toolkit configuration must remain unchanged.

Coverage:
- Pipeline with Jira Toolkit Node runs end-to-end without error
- Jira tool call within the pipeline node returns valid output
- Pipeline output reflects successful Jira data retrieval

## Preconditions

- A Pipeline configured with a Jira Toolkit Node exists in the project
- Logged in as the pipeline owner
- New UI (post-reorganization) deployed

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the existing Pipeline that uses a Jira Toolkit Node | Pipeline opens without error; Jira Toolkit Node is present and configured |
| 2 | Trigger a test run of the pipeline | Pipeline starts executing |
| 3 | Observe the Jira Toolkit Node execution | Node executes without error; outputs valid Jira data |
| 4 | Check pipeline completion | Pipeline completes successfully; final output reflects correct Jira data from the node |

## Expected Final State

Pipeline completes successfully; final output reflects correct Jira data from the node

## Pass/Fail Criteria

PASS:
- Pipeline runs successfully end-to-end
- Jira Toolkit Node executes and returns valid Jira data

FAIL:
- Pipeline fails to start
- Jira Toolkit Node throws an error during pipeline execution
- Pipeline output shows toolkit configuration error
