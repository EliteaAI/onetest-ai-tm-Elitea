---
id: ELITEA-0893
title: "Large DOCX with Many Images Does Not Crash or Silently Truncate"
priority: medium
type: functional
module: pipeline-attachments
status: draft
execution_type: manual
tags: [feat:attachments, feat:artifacts, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4629]
---
# ELITEA-0893: Large DOCX with Many Images Does Not Crash or Silently Truncate

**Module:** Pipeline Attachments · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that `readFile` with `is_capture_image=True` on a DOCX with 10+ embedded images does not crash, hang, or silently truncate the response.

**Coverage:**
- High image count edge case
- No silent truncation — if truncation occurs, it is indicated
- Application remains usable after the response

## Preconditions

- Logged in to dev environment
- Artifact Toolkit with `readFile` + `get_file_metadata` enabled; multimodal LLM configured
- `docx_many_images.docx` (10+ embedded images) in bucket `test`

## Test Data

filename: docx_many_images.docx, bucket: test (10+ embedded images)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call `get_file_metadata` on `docx_many_images.docx`. | `image_count` ≥ 10. All image names listed in `image_names`. |
| 2 | Call `readFile` on `docx_many_images.docx` with `is_capture_image=True`. | Tool call executes. Does not crash or time out with an unhandled error. |
| 3 | Inspect the response for transcription content. | At minimum, partial transcriptions are present. If response is truncated, an indicator or warning is visible — silent truncation is a failure. |
| 4 | Send a follow-up message in the same chat session. | Chat remains responsive. No frozen state, no UI crash, no unresponsive input. |

## Expected Final State

Chat remains responsive. No frozen state, no UI crash, no unresponsive input.

## Pass/Fail Criteria

**Pass:**
- No crash or hang
- Some transcriptions present in response
- Any truncation is explicitly indicated
- Chat remains usable after response

**Fail:**
- Crash, hang, or unhandled timeout
- Completely empty response
- Silent truncation with no indication
- UI becomes unresponsive
