---
id: ELITEA-0817
title: "Pipeline → TestRail: \"Add file to case\" Node Executes End-to-End"
priority: medium
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [feat:image-generation, integration:testrail, feat:toolkits, pipeline]
requirements: [3180]
---
# ELITEA-0817: Pipeline → TestRail: "Add file to case" Node Executes End-to-End

**Module:** Pipelines · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that a Pipeline node using the TestRail 'Add file to case' tool executes end-to-end and the file appears in TestRail.

## Preconditions

- ELITEA Pipelines feature is accessible
- A Pipeline is created with a node configured to invoke TestRail 'Add file to case' tool
- TestRail toolkit is configured with valid credentials
- Artifact bucket contains a file at /my-bucket/pipeline-test.png
- A valid TestRail test case ID is available

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to ELITEA Pipelines and open the pipeline configured with the 'Add file to case' node | Pipeline is visible and ready to execute |
| 2 | Execute the pipeline with case_id and filepath /my-bucket/pipeline-test.png as inputs | Pipeline executes without error; node completes with a success status |
| 3 | Navigate to TestRail and open the test case | pipeline-test.png appears as an attachment on the TestRail test case |

## Expected Final State

pipeline-test.png appears as an attachment on the TestRail test case

## Pass/Fail Criteria

**Pass:** All steps complete as expected.

**Fail:** Any step produces an unexpected result or error.
