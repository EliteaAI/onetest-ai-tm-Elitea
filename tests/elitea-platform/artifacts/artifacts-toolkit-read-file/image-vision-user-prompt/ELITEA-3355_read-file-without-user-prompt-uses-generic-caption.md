---
id: ELITEA-3355
title: "read_file Without user_prompt Uses Generic Caption (Backward Compatibility)"
priority: critical
type: functional
module: artifacts-toolkit-read-file
status: draft
execution_type: manual
tags: [feat:artifacts, feat:image-vision, r-2.0.6, backward-compatibility]
requirements: [EliteaAI/elitea_issues#6530]
---
# ELITEA-3355: read_file Without user_prompt Uses Generic Caption (Backward Compatibility)

**Module:** Artifacts Toolkit Read File · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that `read_file` for an image file without `extra_params` or without `user_prompt` key still uses the generic caption prompt (backward compatibility).

**Coverage:**
- Default behavior unchanged when `user_prompt` not provided
- Generic caption returned for images
- No breaking change for existing agents

## Preconditions

- Logged in to dev environment
- Artifact Toolkit with `read_file` enabled
- Multimodal LLM configured
- `test_image.png` uploaded to bucket `test`

## Test Data

| File | Bucket |
|---|---|
| test_image.png | test |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call `read_file` on `test_image.png` without `extra_params` parameter. | Tool executes successfully. |
| 2 | Examine the response content. | Response is a generic image description/caption, not empty. |
| 3 | Compare with behavior prior to the enhancement. | Behavior matches pre-enhancement: a descriptive caption of what the image contains. |

## Expected Final State

Generic image caption is returned, matching the behavior before the `user_prompt` enhancement was added.

**Note:** Do NOT pass `extra_params={}` (empty object) — this causes a validation error. Simply omit the parameter entirely.

## Pass/Fail Criteria

**Pass:**
- Generic caption returned when `user_prompt` not provided
- No error occurs
- Behavior matches prior release

**Fail:**
- Error when `extra_params` omitted or empty
- No caption returned (blank response)
- Response format changed unexpectedly
