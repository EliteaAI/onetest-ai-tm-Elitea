---
id: ELITEA-0815
title: "Pipeline → QTest: \"Add file to test case\" Node Executes End-to-End"
priority: medium
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [feat:image-generation, integration:qtest, feat:toolkits, pipeline]
requirements: [3180]
---
# ELITEA-0815: Pipeline → QTest: "Add file to test case" Node Executes End-to-End

**Module:** Pipelines · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that a Pipeline node using the QTest 'Add file to test case' tool executes end-to-end and the file appears in QTest.

## Preconditions

- ELITEA Pipelines feature is accessible
- A Pipeline is created with a node configured to invoke QTest 'Add file to test case' tool
- QTest toolkit is configured with valid credentials
- Artifact bucket contains a file at /my-bucket/pipeline-test.png
- A valid QTest test case ID is available

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to ELITEA Pipelines and open the pipeline configured with the 'Add file to test case' node | Pipeline is visible and ready to execute |
| 2 | Execute the pipeline with test_case_id and filepath /my-bucket/pipeline-test.png as inputs | Pipeline executes without error; node completes with a success status |
| 3 | Navigate to QTest and open the test case | pipeline-test.png appears as an attachment on the QTest test case |

## Expected Final State

pipeline-test.png appears as an attachment on the QTest test case

## Pass/Fail Criteria

**Pass:** All steps complete as expected.

**Fail:** Any step produces an unexpected result or error.
