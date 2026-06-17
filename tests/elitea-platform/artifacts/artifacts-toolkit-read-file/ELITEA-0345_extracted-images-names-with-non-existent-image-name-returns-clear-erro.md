---
id: ELITEA-0345
title: "extracted_images_names with Non-Existent Image Name Returns Clear Error"
priority: medium
type: functional
module: artifacts-toolkit-read-file
status: draft
execution_type: manual
tags: [feat:attachments, feat:artifacts, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4629]
---
# ELITEA-0345: extracted_images_names with Non-Existent Image Name Returns Clear Error

**Module:** Artifacts Toolkit Read File · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that specifying a non-existent image name in `extracted_images_names` results in a clear, actionable error message rather than a crash or fabricated output.

**Coverage:**
- Non-existent image name gracefully handled
- No crash or unhandled exception
- No fabricated image description returned
- Tool remains usable after the error

## Preconditions

- Logged in to dev environment
- Artifact Toolkit with `readFile` enabled; multimodal LLM configured
- `docx_with_images.docx` (contains image1.jpeg, image2.png) in bucket `test`

## Test Data

extra_params: {\"extracted_images_names\": [\"nonexistent_image.png\"], \"read_images_only\": true}

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call `readFile` on `docx_with_images.docx` with `is_capture_image=True` and `extra_params` = `{"extracted_images_names": ["nonexistent_image.png"], "read_images_only": true}` as a JSON string. | Tool call executes. A response is returned. |
| 2 | Verify the response contains a clear error or informative message indicating the image was not found. | Error message or empty result with explanation. Not a generic crash dump. |
| 3 | Verify no fabricated image description is returned. | Response does not contain invented image content. |
| 4 | Send a follow-up `readFile` or `get_file_metadata` call in the same session. | Subsequent calls succeed normally. Tool is still functional. |

## Expected Final State

Subsequent calls succeed normally. Tool is still functional.

## Pass/Fail Criteria

**Pass:**
- Clear error returned for non-existent image name
- No crash or unhandled exception
- No fabricated image descriptions
- Tool usable after the error

**Fail:**
- Crash or unhandled exception
- Fabricated image description returned
- Tool unusable after the call
