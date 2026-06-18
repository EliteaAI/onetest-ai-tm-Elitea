---
id: ELITEA-0343
title: "ReadFile with is_capture_image=True Transcribes All Embedded DOCX Images"
priority: medium
type: functional
module: artifacts-toolkit-read-file
status: draft
execution_type: manual
tags: [feat:attachments, feat:artifacts, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4629]
---
# ELITEA-0343: ReadFile with is_capture_image=True Transcribes All Embedded DOCX Images

**Module:** Artifacts Toolkit Read File · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that calling `readFile` with `is_capture_image=True` on a DOCX file transcribes all embedded images via the vision model and includes document text in the response.

**Coverage:**
- All embedded images transcribed
- Transcription count matches `image_count` from `get_file_metadata`
- Document text coexists with image transcriptions in the response

## Preconditions

- Logged in to dev environment
- Artifact Toolkit with `readFile` enabled; multimodal LLM configured (Supports Vision = enabled)
- `docx_with_images.docx` (2 embedded images: image1.jpeg, image2.png) in bucket `test`

## Test Data

filename: docx_with_images.docx, bucket: test, param: is_capture_image=True

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call `readFile` on `docx_with_images.docx` (bucket `test`) with `is_capture_image=True`. | Tool call executes. Response is returned without error. |
| 2 | Verify the response contains transcription content for each of the 2 embedded images. | 2 separate image transcriptions are present. Each contains a description of the image's visual content. |
| 3 | Verify the document text body is also present in the response. | Document text content appears in the response alongside the image transcriptions. |
| 4 | Verify no error messages are returned and the response is complete (not truncated). | No error present. Full response returned. |

## Expected Final State

No error present. Full response returned.

## Pass/Fail Criteria

**Pass:**
- Both images transcribed
- Document text present in response
- No errors returned

**Fail:**
- Any image missing from transcription
- Document text absent
- Error returned or response truncated without indication
