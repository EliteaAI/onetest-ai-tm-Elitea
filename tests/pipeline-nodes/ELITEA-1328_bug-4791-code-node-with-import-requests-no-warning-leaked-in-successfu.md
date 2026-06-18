---
id: ELITEA-1328
title: "[Bug #4791] Code Node with `import requests` — No Warning Leaked in Successful Execution Output"
priority: high
type: functional
module: pipeline-nodes
status: draft
execution_type: manual
tags: [feat:pipeline_nodes, feat:python_sandbox, fix-verification, feat:pipelines, issue:4791, r-2.0.3]
requirements: [4791]
---
# ELITEA-1328: [Bug #4791] Code Node with `import requests` — No Warning Leaked in Successful Execution Output

**Module:** Pipeline Nodes · **Priority:** High · **Type:** Functional

**Objective:** Verify that after the fix for bug #4791, a Code node that imports `requests` does not surface any `RequestsDependencyWarning` (or `urllib3`/`chardet`/`charset_normalizer` warning text) in the pipeline execution output on a successful run. Also verifies that when a declared output variable is used, its value is correctly returned — not replaced by warning text.

## Preconditions

User is logged in to ELITEA.
User has access to the Pipelines section.
A pipeline with at least one Code node is available or can be created.
PR #160 (fix for bug #4791) has been merged and deployed to the environment.

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Pipelines and open or create a pipeline that contains a Code node. | Pipeline editor opens with the Code node visible on the canvas. |
| 2 | Select the Code node and enter the following code: ```python import requests print("ok") ``` Leave no declared output variable (stdout-only). | Code is accepted in the Code node editor without any validation error. |
| 3 | Save the pipeline and run it. | Pipeline executes and the run reaches the Completed state. |
| 4 | Inspect the Code node execution output / pipeline result. | Output contains `ok`. Output does NOT contain any of the following strings: - `RequestsDependencyWarning` - `urllib3` - `chardet` - `charset_normalizer` - `warnings.warn(` |
| 5 | Update the Code node to declare an output variable: ```python import requests result = "done" ``` Set `result` as the declared output variable of the node. | Code node configuration is saved with `result` as the output variable. |
| 6 | Run the pipeline again. | Pipeline executes successfully. |
| 7 | Inspect the output of the Code node and any downstream node that consumes the output variable. | The output variable `result` equals `"done"`. No warning text (`RequestsDependencyWarning`, `urllib3`, etc.) appears in the output variable value or anywhere in the node's execution result. |

## Expected Final State

The output variable `result` equals `"done"`. No warning text (`RequestsDependencyWarning`, `urllib3`, etc.) appears in the output variable value or anywhere in the node's execution result.

## Pass/Fail Criteria

PASS: Output contains only the expected value; no warning text is present in any output field.
FAIL: Any warning text (RequestsDependencyWarning, urllib3, chardet, charset_normalizer) appears in the execution output or is assigned to the output variable.
