---
id: ELITEA-0813
title: "Pipeline → SharePoint: \"Upload file\" Node Executes End-to-End"
priority: medium
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [integration:sharepoint, feat:image-generation, feat:toolkits, pipeline]
requirements: [3180]
---
# ELITEA-0813: Pipeline → SharePoint: "Upload file" Node Executes End-to-End

**Module:** Pipelines · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that a Pipeline node using the SharePoint 'Upload file' tool executes end-to-end and the file appears in SharePoint.

## Preconditions

- ELITEA Pipelines feature is accessible
- A Pipeline is created with a node configured to invoke SharePoint 'Upload file' tool
- SharePoint toolkit is configured with valid credentials
- Artifact bucket contains a file at /my-bucket/pipeline-test.png
- A valid SharePoint site and document library are available

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to ELITEA Pipelines and open the pipeline configured with the 'Upload file' node | Pipeline is visible and ready to execute |
| 2 | Execute the pipeline with the SharePoint target and filepath /my-bucket/pipeline-test.png as inputs | Pipeline executes without error; node completes with a success status |
| 3 | Navigate to the SharePoint document library | pipeline-test.png appears in the SharePoint document library |

## Expected Final State

pipeline-test.png appears in the SharePoint document library

## Pass/Fail Criteria

**Pass:** All steps complete as expected.

**Fail:** Any step produces an unexpected result or error.
