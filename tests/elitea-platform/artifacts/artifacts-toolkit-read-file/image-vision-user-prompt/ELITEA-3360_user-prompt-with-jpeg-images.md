---
id: ELITEA-3360
title: "user_prompt Works for JPEG Images"
priority: high
type: functional
module: artifacts-toolkit-read-file
status: draft
execution_type: manual
tags: [feat:artifacts, feat:image-vision, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6530]
---
# ELITEA-3360: user_prompt Works for JPEG Images

**Module:** Artifacts Toolkit Read File · **Priority:** High · **Type:** Functional

**Objective:** Verify that `user_prompt` works correctly for JPEG images (.jpg and .jpeg extensions), not just PNG.

**Coverage:**
- `.jpg` extension support
- `.jpeg` extension support
- Consistent behavior across JPEG variants

## Preconditions

- Logged in to dev environment
- Artifact Toolkit with `read_file` enabled
- Multimodal LLM configured
- `photo.jpg` and `photo.jpeg` in bucket `test` (images with identifiable content)

## Test Data

| File | Extension | user_prompt |
|---|---|---|
| photo.jpg | .jpg | "How many people are in this image?" |
| photo.jpeg | .jpeg | "What is the main color in this image?" |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call `read_file` on `photo.jpg` with `extra_params={"user_prompt": "How many people are in this image?"}`. | Tool executes. Response answers the question about people count. |
| 2 | Verify response is specific to the question asked. | Response: number or "no people visible" — not a generic description. |
| 3 | Call `read_file` on `photo.jpeg` with a different `user_prompt`. | Tool executes. Response answers the color question. |
| 4 | Confirm both JPEG variants handle `user_prompt` identically to PNG. | Behavior consistent across all image formats. |

## Expected Final State

JPEG images (both .jpg and .jpeg extensions) support `user_prompt` parameter identical to PNG.

## Pass/Fail Criteria

**Pass:**
- Both .jpg and .jpeg work with `user_prompt`
- Responses answer the specific questions
- No format-specific errors

**Fail:**
- .jpg or .jpeg fails with `user_prompt`
- Different behavior between JPEG variants
- JPEG treated differently than PNG
