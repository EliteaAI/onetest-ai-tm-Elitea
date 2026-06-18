---
id: ELITEA-1330
title: "[Bug #4791] Code Node Clean Execution — Baseline, HTTP Request Output, and Consecutive Runs"
priority: medium
type: functional
module: pipeline-nodes
status: draft
execution_type: manual
tags: [feat:pipeline_nodes, feat:python_sandbox, feat:pipelines, issue:4791, r-2.0.3]
requirements: [4791]
---
# ELITEA-1330: [Bug #4791] Code Node Clean Execution — Baseline, HTTP Request Output, and Consecutive Runs

**Module:** Pipeline Nodes · **Priority:** Medium · **Type:** Functional

**Objective:** Verifies Code node output correctness across three complementary scenarios: (1) a baseline arithmetic execution with no imports, (2) a `requests.get()` HTTP call where the response status code is returned as the output variable, and (3) three consecutive runs of the same requests-importing pipeline to confirm no warning accumulation across runs.

## Preconditions

User is logged in to ELITEA.
User has access to the Pipelines section.
A pipeline with a Code node is available or can be created.
The sandbox environment has outbound HTTP access to `https://httpbin.org` (or an equivalent echo endpoint).
PR #160 (fix for bug #4791) has been merged and deployed.

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open or create a pipeline with a Code node. Enter baseline arithmetic code with no imports: ```python x = 2 + 2 print(x) ``` No declared output variable. | Code is accepted. |
| 2 | Run the pipeline. | Pipeline completes successfully. |
| 3 | Inspect the Code node output. | Output shows `4`. No error or warning text is present in the output. |
| 4 | Update the Code node to perform an HTTP GET and assign the result to an output variable: ```python import requests response = requests.get("https://httpbin.org/get") output = response.status_code ``` Set `output` as the declared output variable. | Code is accepted. |
| 5 | Run the pipeline. | Pipeline completes successfully. |
| 6 | Inspect the output variable value. | Output variable `output` equals `200`. No warning text (`RequestsDependencyWarning`, `urllib3`, `chardet`, `charset_normalizer`) is present in any output field. |
| 7 | Update the Code node back to the simple requests import: ```python import requests print("ok") ``` Run the pipeline 3 times consecutively without making any changes between runs. | Each of the 3 runs completes successfully. |
| 8 | Inspect the output of each of the 3 runs. | All 3 runs show `ok` in the output. No run shows any warning text. No accumulation of warning messages across runs. |

## Expected Final State

All 3 runs show `ok` in the output. No run shows any warning text. No accumulation of warning messages across runs.

## Pass/Fail Criteria

PASS: All three scenarios produce the correct output value with no warning text in any run.
FAIL: Any run shows RequestsDependencyWarning or other urllib3/chardet warning text, or the output variable receives warning text instead of the expected value.
