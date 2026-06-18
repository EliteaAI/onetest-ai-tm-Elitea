---
id: ELITEA-0361
title: "read_file on file >200k chars via Pipeline Toolkit Node returns full content — no size limit"
priority: critical
type: functional
module: artifacts-toolkit-read-file
status: ready
execution_type: manual
tags: [feat:artifacts, issue:4011, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#4011]
---
# ELITEA-0361: read_file on file >200k chars via Pipeline Toolkit Node returns full content — no size limit

**Module:** Artifacts Toolkit Read File · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that when read_file is invoked through a Pipeline Toolkit Node, files larger than 200k characters are returned fully with no size-limit constraint.

**Coverage:**
- Pipeline Toolkit Node path does not send `skip_size_check` — function default `True` applies
- File >200k returned in full — no error string
- Pipeline run completes successfully with full file content in output

## Preconditions

- Logged in to {{base_url}} with Editor or Admin role
- A Pipeline with a Toolkit Node configured with the Artifact Toolkit
- Test file `xlarge_file.txt` (~300k chars) pre-uploaded to the bucket

## Test Data

- File: `xlarge_file.txt` (~300,000 chars)
- Pipeline: Toolkit Node → read_file → Printer Node (to show output)
- Toolkit Node input: `filename = xlarge_file.txt`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the Pipelines page. Open the Pipeline containing the Artifact Toolkit Node configured to call read_file on `xlarge_file.txt`. | Pipeline editor opens. |
| 2 | Run the pipeline. | Pipeline execution starts. |
| 3 | Inspect the Run Details / output of the Toolkit Node. | Full file content (~300k chars) is present in the node output. No size-limit error string appears. |

## Expected Final State

Full file content (~300k chars) is present in the node output. No size-limit error string appears.

## Pass/Fail Criteria

**Pass:**
- Full file content returned in Pipeline Toolkit Node output
- No `[Content has N lines and exceeds size limit...]` error string

**Fail:**
- Size-limit error string appears in the Toolkit Node output
- Pipeline fails or returns truncated content
