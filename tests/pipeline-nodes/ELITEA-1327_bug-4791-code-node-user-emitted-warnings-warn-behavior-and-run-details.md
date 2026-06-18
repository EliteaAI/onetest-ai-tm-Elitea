---
id: ELITEA-1327
title: "[Bug #4791] Code Node — User-Emitted warnings.warn() Behavior and Run Details Cleanliness"
priority: medium
type: functional
module: pipeline-nodes
status: draft
execution_type: manual
tags: [feat:pipeline_nodes, feat:python_sandbox, feat:pipelines, issue:4791, r-2.0.3]
requirements: [4791]
---
# ELITEA-1327: [Bug #4791] Code Node — User-Emitted warnings.warn() Behavior and Run Details Cleanliness

**Module:** Pipeline Nodes · **Priority:** Medium · **Type:** Functional

**Objective:** Covers two complementary post-fix scenarios: (1) a Code node that explicitly calls `warnings.warn()` from user code — verifying that the stdout result is still returned and no unexpected error is shown regardless of whether the user warning is surfaced or suppressed; (2) inspection of Run Details for a completed run that imports `requests` — confirming no `error` field or warning text appears in the execution record at the Code node step.

## Preconditions

User is logged in to ELITEA.
User has access to the Pipelines section.
A pipeline with a Code node is available or can be created.
PR #160 (fix for bug #4791) has been merged and deployed.

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open or create a pipeline with a Code node. Enter code that explicitly emits a user warning: ```python import warnings warnings.warn("custom-user-warning") print("result") ``` No declared output variable. | Code is accepted in the editor. |
| 2 | Run the pipeline. | Pipeline completes successfully (status = Completed, not Failed). |
| 3 | Inspect the Code node execution output. | The stdout value `result` is returned as the node output. No unexpected Python exception or misleading error message is displayed to the user. Note: The user warning string (`custom-user-warning`) may or may not be visible — both outcomes are acceptable. What is NOT acceptable: the run failing, or the output variable receiving the warning string instead of `result`. |
| 4 | Update the Code node to use `import requests; print("ok")`. Run the pipeline to completion. | Pipeline completes successfully. |
| 5 | Open the Run Details panel for the completed run (via the pipeline run history or the execution chipset). | Run Details panel opens showing individual node steps. |
| 6 | Locate the Code node step in the Run Details and expand its execution record. | The Code node step record shows: - Execution status: success/completed - No `error` field with warning text - No `RequestsDependencyWarning`, `urllib3`, `chardet`, or `charset_normalizer` text anywhere in the step record - stdout output (`ok`) is present if shown |

## Expected Final State

The Code node step record shows: - Execution status: success/completed - No `error` field with warning text - No `RequestsDependencyWarning`, `urllib3`, `chardet`, or `charset_normalizer` text anywhere in the step record - stdout output (`ok`) is present if shown

## Pass/Fail Criteria

PASS: `result` is returned as stdout output; no unexpected failure; Run Details shows no warning text in the Code node step record.
FAIL: Pipeline fails due to the user warning, the output variable receives warning text instead of `result`, or Run Details shows RequestsDependencyWarning / urllib3 / chardet text in the Code node step.
