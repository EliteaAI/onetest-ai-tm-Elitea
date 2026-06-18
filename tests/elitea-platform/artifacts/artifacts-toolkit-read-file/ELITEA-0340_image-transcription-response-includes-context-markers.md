---
id: ELITEA-0340
title: "Image Transcription Response Includes Context Markers"
priority: medium
type: functional
module: artifacts-toolkit-read-file
status: draft
execution_type: manual
tags: [feat:attachments, feat:artifacts, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4629]
---
# ELITEA-0340: Image Transcription Response Includes Context Markers

**Module:** Artifacts Toolkit Read File · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that when multiple images are transcribed in a single `readFile` response, each transcription section includes a unique context marker (e.g. image filename, index, or positional label) allowing the caller to distinguish between them.

**Coverage:**
- Each transcription block has a unique identifier
- Identifiers are distinct across images
- Format supports programmatic or manual disambiguation

## Preconditions

- Logged in to dev environment
- Artifact Toolkit with `readFile` enabled; multimodal LLM configured
- `docx_with_images.docx` (2 embedded images: image1.jpeg, image2.png) in bucket `test`

## Test Data

filename: docx_with_images.docx, bucket: test, param: is_capture_image=True

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call `readFile` on `docx_with_images.docx` with `is_capture_image=True`. | Response returned. Two image transcription sections present. |
| 2 | Locate each image transcription block in the response. | Two distinct transcription sections are identifiable. |
| 3 | Verify each section includes an identifier — filename, index number, or positional marker (e.g. "image1.jpeg:", "Image 1:", "[image2.png]"). | At least one unique identifier present per transcription block. |
| 4 | Verify the identifiers are unique (no two sections share the same label). | Each transcription section has a distinct identifier. The two cannot be confused. |

## Expected Final State

Each transcription section has a distinct identifier. The two cannot be confused.

## Pass/Fail Criteria

**Pass:**
- Each transcription has a unique identifier
- Sections clearly distinguishable

**Fail:**
- No identifiers present
- Both sections use the same label
- Impossible to determine which transcription corresponds to which image
