---
id: ELITEA-0338
title: "ReadFile with extracted_images_names + read_images_only=True in extra_params Returns Selective Image-Only Transcription"
priority: medium
type: functional
module: artifacts-toolkit-read-file
status: draft
execution_type: manual
tags: [feat:attachments, feat:artifacts, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4629]
---
# ELITEA-0338: ReadFile with extracted_images_names + read_images_only=True in extra_params Returns Selective Image-Only Transcription

**Module:** Artifacts Toolkit Read File · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that passing `extracted_images_names` and `read_images_only=true` inside `extra_params` (as a JSON string) causes `readFile` to return only the specified image transcriptions, with document text suppressed.

**Coverage:**
- Selective transcription of named images only
- Document text suppression when `read_images_only=true`
- `extra_params` accepted as a JSON string
- Behavior when `read_images_only=false` (both images + text returned)

## Preconditions

- Logged in to dev environment
- Artifact Toolkit with `readFile` enabled; multimodal LLM configured
- `docx_with_images.docx` (image1.jpeg, image2.png) in bucket `test`

## Test Data

| Scenario | extra_params (JSON string) | Expected |
|---|---|---|
| A | {\"extracted_images_names\": [\"image1.jpeg\"], \"read_images_only\": true} | image1.jpeg transcribed only; no document text |
| B | {\"extracted_images_names\": [\"image1.jpeg\", \"image2.png\"], \"read_images_only\": false} | Both images transcribed; document text also present |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call `readFile` on `docx_with_images.docx` with `is_capture_image=True` and `extra_params` = `{"extracted_images_names": ["image1.jpeg"], "read_images_only": true}` passed as a JSON string. | Tool call executes. Response returned. |
| 2 | Verify only `image1.jpeg` is transcribed. | Transcription for `image1.jpeg` is present. No transcription for `image2.png`. |
| 3 | Verify document text is suppressed. | No document text body in the response. Only image transcription content. |
| 4 | Repeat with Scenario B: `extra_params` = `{"extracted_images_names": ["image1.jpeg", "image2.png"], "read_images_only": false}` as a JSON string. | Both images transcribed. Document text also present in the response. |

## Expected Final State

Both images transcribed. Document text also present in the response.

## Pass/Fail Criteria

**Pass:**
- Scenario A: only specified image transcribed, document text suppressed
- Scenario B: both images and document text present

**Fail:**
- Wrong images transcribed
- Document text appears when `read_images_only=true`
- `extra_params` rejected or JSON string format causes error
