---
id: ELITEA-0899
title: "Attached File Visible in Pipeline Run History and Details"
priority: high
type: functional
module: pipeline-attachments
status: draft
execution_type: manual
tags: [feat:attachments, feat:artifacts, feat:pipelines, nfr:usability, eng:frontend, feature:4766, eng:backend, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4766]
---
# ELITEA-0899: Attached File Visible in Pipeline Run History and Details

**Module:** Pipeline Attachments · **Priority:** High · **Type:** Functional

**Objective:** Verify that after a pipeline run with a file attached, the attached file is traceable in run history — visible as a file path in the `read_multiple_files` tool call artifact of the LLM node.

**Coverage:**
- Run history entry created after pipeline chat execution with attachment
- read_multiple_files tool call artifact present for the LLM node
- INPUT file_paths contains the attached file path with correct filename and bucket

## Preconditions

- Logged in — Private project
- Pipeline with Allow Attachments enabled, at least one previous run completed with a file attached

## Test Data

- File: sample.pdf

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the pipeline test chat. Attach sample.pdf, type a prompt, and click Send. | Pipeline run executes and completes. |
| 2 | Click the view run history button in the pipeline test chat header. | Run history panel opens listing past runs. |
| 3 | Click the most recent run entry. | Run details open showing the timeline with execution steps. |
| 4 | Browse through the steps in the timeline and inspect their details. | At least one step contains the file path and filename sample.pdf — confirming the attachment was present during the pipeline execution. |

## Expected Final State

At least one step contains the file path and filename sample.pdf — confirming the attachment was present during the pipeline execution.

## Pass/Fail Criteria

**Pass:**
- Run history entry created for the file-attached run
- sample.pdf reference visible in run details

**Fail:**
- No run history entry created
- File name absent from run details
