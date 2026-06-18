---
id: ELITEA-1162
title: "TC-019 (Confluence): Pipeline Using Confluence Toolkit Node Executes Successfully After UI Reorganization"
priority: medium
type: functional
module: confluence-toolkit-configuration
status: draft
execution_type: manual
tags: [int:confluence, feat:toolkits, issue:4029, r-2.0.2]
requirements: [ProjectAlita/projectalita.github.io#4029]
---
# ELITEA-1162: TC-019 (Confluence): Pipeline Using Confluence Toolkit Node Executes Successfully After UI Reorganization

**Module:** Confluence Toolkit Configuration · **Priority:** Medium · **Type:** Functional

**Objective:** Regression test — verify that a Pipeline that uses a Confluence Toolkit Node continues to execute successfully after the UI reorganization is deployed. The backend API contract for toolkit configuration must remain unchanged.

Coverage:
- Pipeline with Confluence Toolkit Node runs end-to-end without error
- Confluence tool call within the pipeline node returns valid output
- Pipeline output reflects successful Confluence data retrieval

## Preconditions

- A Pipeline configured with a Confluence Toolkit Node exists in the project
- Logged in as the pipeline owner
- New UI (post-reorganization) deployed

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the existing Pipeline that uses a Confluence Toolkit Node | Pipeline opens without error; Confluence Toolkit Node is present and configured |
| 2 | Trigger a test run of the pipeline | Pipeline starts executing |
| 3 | Observe the Confluence Toolkit Node execution | Node executes without error; outputs valid Confluence data (pages, search results) |
| 4 | Check pipeline completion | Pipeline completes successfully; final output reflects correct Confluence data from the node |

## Expected Final State

Pipeline completes successfully; final output reflects correct Confluence data from the node

## Pass/Fail Criteria

PASS:
- Pipeline runs successfully end-to-end
- Confluence Toolkit Node executes and returns valid Confluence data

FAIL:
- Pipeline fails to start
- Confluence Toolkit Node throws an error during pipeline execution
- Pipeline output shows toolkit configuration error
