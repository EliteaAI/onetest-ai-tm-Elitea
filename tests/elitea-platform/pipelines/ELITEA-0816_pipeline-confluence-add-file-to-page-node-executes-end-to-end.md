---
id: ELITEA-0816
title: "Pipeline → Confluence: \"Add file to page\" Node Executes End-to-End"
priority: medium
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [integration:confluence, feat:image-generation, feat:toolkits, pipeline]
requirements: [3180]
---
# ELITEA-0816: Pipeline → Confluence: "Add file to page" Node Executes End-to-End

**Module:** Pipelines · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that a Pipeline node using the Confluence 'Add file to page' tool executes end-to-end and the file appears in Confluence.

## Preconditions

- ELITEA Pipelines feature is accessible
- A Pipeline is created with a node configured to invoke Confluence 'Add file to page' tool
- Confluence toolkit is configured with valid credentials
- Artifact bucket contains a file at /my-bucket/pipeline-test.png
- A valid Confluence page ID is available

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to ELITEA Pipelines and open the pipeline configured with the 'Add file to page' node | Pipeline is visible and ready to execute |
| 2 | Execute the pipeline with page_id and filepath /my-bucket/pipeline-test.png as inputs | Pipeline executes without error; node completes with a success status |
| 3 | Navigate to Confluence and open the page | pipeline-test.png appears on the Confluence page |

## Expected Final State

pipeline-test.png appears on the Confluence page

## Pass/Fail Criteria

**Pass:** All steps complete as expected.

**Fail:** Any step produces an unexpected result or error.
