---
id: ELITEA-0363
title: "read_file on file >200k chars via Toolkit Test Settings returns full content — no size limit"
priority: high
type: functional
module: artifacts-toolkit-read-file
status: ready
execution_type: manual
tags: [feat:artifacts, issue:4011, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#4011]
---
# ELITEA-0363: read_file on file >200k chars via Toolkit Test Settings returns full content — no size limit

**Module:** Artifacts Toolkit Read File · **Priority:** High · **Type:** Functional

**Objective:** Verify that calling read_file directly from the Toolkit Test Settings panel on a file exceeding 200k characters returns the full content with no size-limit constraint.

**Coverage:**
- Direct Toolkit Test Settings path uses function default `skip_size_check=True`
- File >200k returned in full
- No size-limit error string in the test panel response

## Preconditions

- Logged in to {{base_url}} with Editor or Admin role
- An Artifact Toolkit configured and accessible via Toolkits page
- Test file `xlarge_file.txt` (~300k chars) pre-uploaded to the toolkit's bucket

## Test Data

- File: `xlarge_file.txt` (~300,000 chars)
- Tool: `read_file`
- Parameter: `filename = xlarge_file.txt`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Toolkits page. Open the Artifact Toolkit. Go to the Test Settings panel. | Toolkit Test Settings panel opens with available tools listed. |
| 2 | Select the `read_file` tool. Enter `filename = xlarge_file.txt`. Click Run. | Tool executes. |
| 3 | Inspect the response in the test panel. | Full file content (~300k chars) returned. No `[Content has N lines and exceeds size limit...]` error string. |

## Expected Final State

Full file content (~300k chars) returned. No `[Content has N lines and exceeds size limit...]` error string.

## Pass/Fail Criteria

**Pass:**
- Full content returned in Toolkit Test Settings panel
- No size-limit error string in response

**Fail:**
- Size-limit error string returned
- Response truncated or empty
