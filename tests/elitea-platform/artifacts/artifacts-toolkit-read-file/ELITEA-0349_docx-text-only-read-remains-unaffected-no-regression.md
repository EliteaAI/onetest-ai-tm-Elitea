---
id: ELITEA-0349
title: "DOCX Text-Only Read Remains Unaffected (No Regression)"
priority: medium
type: functional
module: artifacts-toolkit-read-file
status: draft
execution_type: manual
tags: [feat:attachments, feat:artifacts, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4629]
---
# ELITEA-0349: DOCX Text-Only Read Remains Unaffected (No Regression)

**Module:** Artifacts Toolkit Read File · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that `readFile` on a DOCX file without any image parameters continues to return text content only, with no image processing triggered.

**Coverage:**
- `readFile` default behavior unchanged
- No accidental image processing when image params are absent
- DOCX files with and without embedded images both unaffected

## Preconditions

- Logged in to dev environment
- Artifact Toolkit with `readFile` enabled
- `docx_with_images.docx` and `docx_text_only.docx` in bucket `test`

## Test Data

Both files in bucket `test`, called without `is_capture_image` or `extra_params`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call `readFile` on `docx_with_images.docx` without any image parameters (no `is_capture_image`, no `extra_params`). | Tool executes. Response contains document text content only. |
| 2 | Verify no image transcriptions appear in the response. | Response contains only document text. No image-related content or vision model output. |
| 3 | Verify no errors are returned. | Clean response without error messages or warnings. |
| 4 | Repeat steps 1–3 for `docx_text_only.docx`. | Same result: text returned, no crash, no image-related messages. |

## Expected Final State

Same result: text returned, no crash, no image-related messages.

## Pass/Fail Criteria

**Pass:**
- Text-only responses for both files
- No image processing triggered
- No errors

**Fail:**
- Any image transcription appears without being requested
- Error on files that previously read successfully
- Behavior changed from prior baseline
