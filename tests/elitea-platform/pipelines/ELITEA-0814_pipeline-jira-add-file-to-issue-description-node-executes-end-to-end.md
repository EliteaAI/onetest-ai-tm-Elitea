---
id: ELITEA-0814
title: "Pipeline → Jira: \"Add file to issue description\" Node Executes End-to-End"
priority: medium
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [feat:image-generation, integration:jira, feat:toolkits, pipeline]
requirements: [3180]
---
# ELITEA-0814: Pipeline → Jira: "Add file to issue description" Node Executes End-to-End

**Module:** Pipelines · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that a Pipeline node using the Jira 'Add file to issue description' tool executes end-to-end and the file appears in the Jira issue.

## Preconditions

- ELITEA Pipelines feature is accessible
- A Pipeline is created with a node configured to invoke Jira 'Add file to issue description' tool
- Jira toolkit is configured with valid credentials
- Artifact bucket contains a file at /my-bucket/pipeline-test.png
- A valid Jira issue key is available (e.g., PROJ-123)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to ELITEA Pipelines and open the pipeline configured with the 'Add file to issue description' node | Pipeline is visible and ready to execute |
| 2 | Execute the pipeline with issue_key and filepath /my-bucket/pipeline-test.png as inputs | Pipeline executes without error; node completes with a success status |
| 3 | Navigate to Jira and open the issue | pipeline-test.png reference appears in the Jira issue description |

## Expected Final State

pipeline-test.png reference appears in the Jira issue description

## Pass/Fail Criteria

**Pass:** All steps complete as expected.

**Fail:** Any step produces an unexpected result or error.
