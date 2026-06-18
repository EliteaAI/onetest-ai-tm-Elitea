---
id: ELITEA-1329
title: "[Bug #4791] Code Node — Runtime Errors (ZeroDivisionError, NameError, SyntaxError) Still Surface After Fix"
priority: high
type: functional
module: pipeline-nodes
status: draft
execution_type: manual
tags: [feat:pipeline_nodes, feat:python_sandbox, error-regression, feat:pipelines, issue:4791, r-2.0.3]
requirements: [4791]
---
# ELITEA-1329: [Bug #4791] Code Node — Runtime Errors (ZeroDivisionError, NameError, SyntaxError) Still Surface After Fix

**Module:** Pipeline Nodes · **Priority:** High · **Type:** Functional

**Objective:** Regression verification that the fix for bug #4791 (gating stderr→error propagation on `result.status == 'error'`) does NOT suppress genuine Python runtime errors. Covers ZeroDivisionError, NameError, and SyntaxError — all three must still surface a clear error/traceback message in the pipeline output after the fix.

## Preconditions

User is logged in to ELITEA.
User has access to the Pipelines section.
A pipeline with a Code node is available or can be created.
PR #160 (fix for bug #4791) has been merged and deployed to the environment.

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open or create a pipeline with a Code node. Enter the following code that will raise a `ZeroDivisionError`: ```python result = 1 / 0 ``` | Code is accepted in the editor. |
| 2 | Run the pipeline. | Pipeline run fails (does not reach Completed status). |
| 3 | Inspect the Code node execution output. | Output shows a clear error message referencing `ZeroDivisionError` or `division by zero`. The error is NOT silently suppressed or replaced with an empty/blank result. |
| 4 | Update the Code node code to trigger a `NameError`: ```python print(undefined_var) ``` | Code is accepted in the editor. |
| 5 | Run the pipeline. | Pipeline run fails. |
| 6 | Inspect the Code node execution output. | Output shows a clear error message referencing `NameError` and `undefined_var`. Error is not suppressed. |
| 7 | Update the Code node code to contain a `SyntaxError`: ```python def broken(: pass ``` | Code is accepted in the editor (syntax checking may be deferred to runtime). |
| 8 | Run the pipeline. | Pipeline run fails. |
| 9 | Inspect the Code node execution output. | Output shows a clear error message referencing `SyntaxError`. Error is not suppressed or hidden. |

## Expected Final State

Output shows a clear error message referencing `SyntaxError`. Error is not suppressed or hidden.

## Pass/Fail Criteria

PASS: All three error types (ZeroDivisionError, NameError, SyntaxError) surface in the output with identifiable error text.
FAIL: Any error is silently swallowed, or the output shows a blank/missing result instead of an error message.
