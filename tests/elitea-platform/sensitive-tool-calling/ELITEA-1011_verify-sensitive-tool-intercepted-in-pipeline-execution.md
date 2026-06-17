---
id: ELITEA-1011
title: "Verify Sensitive Tool Intercepted in Pipeline Execution"
priority: critical
type: functional
module: sensitive-tool-calling
status: ready
execution_type: manual
tags: [user_story:3780, feat:agents, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3780]
---
# ELITEA-1011: Verify Sensitive Tool Intercepted in Pipeline Execution

**Module:** Sensitive Tool Calling · **Priority:** Critical · **Type:** Functional

**Objective:** Verify the middleware intercepts a sensitive tool invocation occurring within a Pipeline step, pausing execution until the user responds.

## Preconditions

- github > create_pull_request configured as sensitive
- A Pipeline exists with an agent step that calls the GitHub create_pull_request tool

## Test Data

- Pipeline containing a step that triggers github.create_pull_request

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the Pipeline page. Start a pipeline run with a prompt that triggers the GitHub create_pull_request tool. | Pipeline begins execution. |
| 2 | Observe the pipeline execution UI. | Execution pauses and authorization dialog appears before the tool step runs. |
| 3 | Click [Authorize]. | Dialog closes. Pipeline tool step executes. Pipeline continues to completion. |
| 4 | Run the pipeline again and click [Block] when the dialog appears. | Tool step does NOT execute. Pipeline receives the blocked result. Agent step produces a response acknowledging it. |

## Expected Final State

Tool step does NOT execute. Pipeline receives the blocked result. Agent step produces a response acknowledging it.

## Pass/Fail Criteria

Pass:
- Authorization dialog appears during pipeline execution
- Authorize allows pipeline to continue with the tool executing
- Block prevents the tool step from executing; pipeline handles it gracefully

Fail:
- Tool executes in pipeline without dialogs
- Pipeline crashes or hangs indefinitely after Block
