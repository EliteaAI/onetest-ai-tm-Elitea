---
id: ELITEA-0347
title: "get_file_metadata Returns Embedded Image Metadata for DOCX Files"
priority: medium
type: functional
module: artifacts-toolkit-read-file
status: draft
execution_type: manual
tags: [feat:attachments, feat:artifacts, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4629]
---
# ELITEA-0347: get_file_metadata Returns Embedded Image Metadata for DOCX Files

**Module:** Artifacts Toolkit Read File · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that `get_file_metadata` returns a correctly structured JSON response with embedded image metadata for DOCX files, and returns `image_count=0` for DOCX files without embedded images.

**Coverage:**
- Full JSON schema of `get_file_metadata` response
- Presence of `instruction_for_readFile` block with all sub-fields
- `image_count` and `image_names` accuracy
- Graceful response for DOCX without images

## Preconditions

- Logged in to dev environment
- Artifact Toolkit configured with `get_file_metadata` enabled; multimodal LLM set (Supports Vision = enabled)
- `docx_with_images.docx` (2 embedded images: image1.jpeg, image2.png) uploaded to bucket `test`
- `docx_text_only.docx` (no embedded images) uploaded to bucket `test`

## Test Data

| File | Bucket | Expected image_count |
|---|---|---|
| docx_with_images.docx | test | 2 |
| docx_text_only.docx | test | 0 |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | In a chat session with Artifact Toolkit active, instruct the LLM to call `get_file_metadata` on `docx_with_images.docx` in bucket `test`. | Tool call executes. A JSON response object is returned. |
| 2 | Verify the top-level fields: `filename`, `type`, `extension`, `filesize`, `image_count`, `image_names`, `bucket`, `status`. | All fields are present. `status` = "success". `image_count` = 2. `image_names` contains 2 entries matching the embedded image filenames. `bucket` = "test". |
| 3 | Verify the `instruction_for_readFile` block contains: `first_class_params.is_capture_image`, `extra_params.extracted_images_names`, `extra_params.read_images_only`, `extra_params.prompt`, and `notes`. | All sub-fields are present with descriptive guidance text. `notes` mentions passing `extra_params` as a JSON string. |
| 4 | Call `get_file_metadata` on `docx_text_only.docx` in bucket `test`. | Response returned. `status` = "success". `image_count` = 0. `image_names` = []. No crash or error. |

## Expected Final State

Response returned. `status` = "success". `image_count` = 0. `image_names` = []. No crash or error.

## Pass/Fail Criteria

**Pass:**
- All top-level fields present and correct
- `instruction_for_readFile` block complete with all sub-fields
- `docx_text_only.docx` returns `image_count=0` without error

**Fail:**
- Any field missing from the response
- Wrong `image_count` value
- Crash or unhandled exception on either file
