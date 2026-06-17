---
id: ELITEA-0352
title: "File uploaded via Artifacts page (300k chars) then read via Pipeline Toolkit Node — full content returned"
priority: high
type: functional
module: artifacts-toolkit-read-file
status: ready
execution_type: manual
tags: [feat:artifacts, issue:4011, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#4011]
---
# ELITEA-0352: File uploaded via Artifacts page (300k chars) then read via Pipeline Toolkit Node — full content returned

**Module:** Artifacts Toolkit Read File · **Priority:** High · **Type:** Functional

**Objective:** Verify that a file exceeding 200k chars uploaded via the Artifacts page can be read fully when accessed via a Pipeline Toolkit Node — confirming that the pipeline path has no size limit.

**Coverage:**
- File >200k uploaded successfully via Artifacts page
- Pipeline Toolkit Node reads the file with no size constraint
- Full ~300k content flows into the pipeline output

## Preconditions

- Logged in to {{base_url}} with Editor or Admin role
- Artifacts page accessible
- A Pipeline with a Toolkit Node configured with the Artifact Toolkit pointing to the same bucket
- Local file `xlarge_file.txt` (~300k chars) prepared for upload

## Test Data

- File to upload: `xlarge_file.txt` (~300,000 chars)
- Target bucket: the bucket configured on the Pipeline's Artifact Toolkit Node
- Pipeline: Toolkit Node → read_file (`xlarge_file.txt`) → Printer Node

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the Artifacts page. Upload `xlarge_file.txt` (~300k chars) to the target bucket. | Upload completes. File appears in the bucket. |
| 2 | Navigate to the Pipelines page. Open the Pipeline with the Artifact Toolkit Node configured to read `xlarge_file.txt`. | Pipeline editor opens. |
| 3 | Run the pipeline. | Execution starts. |
| 4 | Inspect Run Details for the Toolkit Node output. | Full ~300k content present in output. No size-limit error string. |

## Expected Final State

Full ~300k content present in output. No size-limit error string.

## Pass/Fail Criteria

**Pass:**
- File uploads successfully
- Pipeline Toolkit Node returns full content of the 300k file
- No size-limit error in Run Details

**Fail:**
- Upload fails
- Toolkit Node returns size-limit error for the 300k file
- Content truncated in pipeline output
