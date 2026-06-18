---
id: ELITEA-0342
title: "Existing is_capture_image=True for Standalone Image Files Not Broken"
priority: medium
type: functional
module: artifacts-toolkit-read-file
status: draft
execution_type: manual
tags: [feat:attachments, feat:artifacts, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4629]
---
# ELITEA-0342: Existing is_capture_image=True for Standalone Image Files Not Broken

**Module:** Artifacts Toolkit Read File · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that `readFile` with `is_capture_image=True` continues to work correctly for standalone image files (PNG, JPG) as a regression check after the DOCX image extraction feature is introduced.

**Coverage:**
- `.png` file: `is_capture_image=True` returns image description
- `.jpg` file: `is_capture_image=True` returns image description
- No regression from DOCX feature additions

## Preconditions

- Logged in to dev environment
- Artifact Toolkit with `readFile` enabled; multimodal LLM configured
- `test_image.png` and `test_image.jpg` in bucket `test`

## Test Data

| File | Bucket |
|---|---|
| test_image.png | test |
| test_image.jpg | test |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call `readFile` on `test_image.png` (bucket `test`) with `is_capture_image=True`. | Tool executes. A descriptive transcription of the image content is returned. No error. |
| 2 | Call `readFile` on `test_image.jpg` (bucket `test`) with `is_capture_image=True`. | Tool executes. A descriptive transcription of the image content is returned. No error. |
| 3 | Verify both responses contain meaningful image descriptions consistent with prior behavior. | Image descriptions are present, relevant, and contain no error messages. |

## Expected Final State

Image descriptions are present, relevant, and contain no error messages.

## Pass/Fail Criteria

**Pass:**
- Both standalone image files return valid transcriptions without error

**Fail:**
- Any previously working image type now fails or returns an error
