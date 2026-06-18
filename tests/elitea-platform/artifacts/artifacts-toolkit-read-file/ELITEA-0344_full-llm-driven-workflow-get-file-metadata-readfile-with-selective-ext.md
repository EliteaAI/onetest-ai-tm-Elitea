---
id: ELITEA-0344
title: "Full LLM-Driven Workflow: get_file_metadata → readFile with Selective Extraction"
priority: medium
type: functional
module: artifacts-toolkit-read-file
status: draft
execution_type: manual
tags: [feat:attachments, feat:artifacts, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4629]
---
# ELITEA-0344: Full LLM-Driven Workflow: get_file_metadata → readFile with Selective Extraction

**Module:** Artifacts Toolkit Read File · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that an LLM with access to the Artifact Toolkit autonomously uses the two-step workflow — calling `get_file_metadata` first to discover images, then calling `readFile` with selective `extracted_images_names` in `extra_params` — without explicit user instruction on parameters.

**Coverage:**
- LLM-initiated tool chain: `get_file_metadata` → `readFile`
- Correct propagation of `image_names` from metadata into `extracted_images_names`
- `extra_params` passed as JSON string in the tool call
- Final response quality

## Preconditions

- Logged in to dev environment
- Artifact Toolkit with `readFile` + `get_file_metadata` enabled; multimodal LLM configured
- `docx_with_images.docx` in bucket `test`

## Test Data

Prompt: "Describe the images embedded in docx_with_images.docx in bucket test."

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | In a chat with Artifact Toolkit, send: "Describe the images embedded in docx_with_images.docx in bucket test." Do NOT specify parameters. | LLM begins processing. |
| 2 | Verify the LLM calls `get_file_metadata` first. | `get_file_metadata` tool call is visible in the response trace or tool output. Metadata JSON with image names is returned. |
| 3 | Verify the LLM then calls `readFile` using the image names from step 2 inside `extra_params` as a JSON string. | `readFile` tool call includes `extracted_images_names` populated from the metadata response. `extra_params` is a JSON string. |
| 4 | Verify the final LLM response includes meaningful image descriptions. | LLM provides image descriptions derived from vision transcription. |

## Expected Final State

LLM provides image descriptions derived from vision transcription.

## Pass/Fail Criteria

**Pass:**
- Two-step tool chain executed autonomously
- Image names propagated correctly from metadata to readFile
- Meaningful transcription returned in final response

**Fail:**
- LLM calls `readFile` without first calling `get_file_metadata`
- `extra_params` not passed as JSON string
- No image descriptions in final response
