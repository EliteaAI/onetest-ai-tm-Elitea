---
id: ELITEA-0341
title: "DOCX Image Transcription via Pipeline Toolkit Node"
priority: medium
type: functional
module: artifacts-toolkit-read-file
status: draft
execution_type: manual
tags: [feat:attachments, feat:artifacts, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4629]
---
# ELITEA-0341: DOCX Image Transcription via Pipeline Toolkit Node

**Module:** Artifacts Toolkit Read File · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that DOCX image transcription works correctly when triggered through a Pipeline's Toolkit Node.

**Coverage:**
- `readFile` with `is_capture_image=True` works inside a pipeline Toolkit Node
- Pipeline completes without error
- Image transcription output visible in pipeline run results

## Preconditions

- Logged in to dev environment
- Pipeline exists with a Toolkit Node configured for Artifact Toolkit + multimodal LLM
- `docx_with_images.docx` in bucket `test`

## Test Data

Pipeline with Toolkit Node targeting `readFile` on `docx_with_images.docx`, bucket: `test`, `is_capture_image=True`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the pipeline. Configure the Toolkit Node to call `readFile` on `docx_with_images.docx` (bucket `test`) with `is_capture_image=True`. | Configuration saved successfully. |
| 2 | Run the pipeline. | Pipeline starts. No immediate failure. |
| 3 | Wait for the pipeline run to complete. | Pipeline run reaches a completed state. |
| 4 | Inspect the Toolkit Node output in the pipeline run results. | Output contains image transcription content for the 2 embedded images. No error messages. |

## Expected Final State

Output contains image transcription content for the 2 embedded images. No error messages.

## Pass/Fail Criteria

**Pass:**
- Pipeline completes successfully
- Toolkit Node output contains image transcriptions

**Fail:**
- Pipeline errors out or hangs
- Toolkit Node output is empty or contains an error message
