---
id: ELITEA-3357
title: "get_file_metadata Advertises user_prompt for Image Extensions"
priority: critical
type: functional
module: artifacts-toolkit-read-file
status: draft
execution_type: manual
tags: [feat:artifacts, feat:image-vision, r-2.0.6, discoverability]
requirements: [EliteaAI/elitea_issues#6530]
---
# ELITEA-3357: get_file_metadata Advertises user_prompt for Image Extensions

**Module:** Artifacts Toolkit Read File · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that `get_file_metadata()` for image file extensions (PNG, JPG, JPEG, GIF, etc.) advertises the `user_prompt` parameter in the response, enabling LLM discovery.

**Coverage:**
- `get_file_metadata` response includes `user_prompt` for image types
- LLM can discover the feature autonomously
- Parameter documentation in metadata is accurate

## Preconditions

- Logged in to dev environment
- Artifact Toolkit with `get_file_metadata` enabled
- Various image files in bucket `test`: `image.png`, `image.jpg`, `image.jpeg`, `image.gif`

## Test Data

| File Extension | Expected user_prompt in metadata |
|---|---|
| .png | Yes |
| .jpg | Yes |
| .jpeg | Yes |
| .gif | Yes |
| .txt | No |
| .pdf | No |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call `get_file_metadata` on `image.png` in bucket `test`. | Metadata response returned. |
| 2 | Examine the response for available parameters. | Response lists `user_prompt` as an available parameter in `extra_params`. |
| 3 | Repeat for `image.jpg`, `image.jpeg`, `image.gif`. | All image types show `user_prompt` in available parameters. |
| 4 | Call `get_file_metadata` on a `.txt` file. | Metadata returned, `user_prompt` NOT listed (or clearly marked as image-only). |
| 5 | Verify the parameter description is clear and useful. | Description explains purpose: "Custom prompt for image vision analysis" or similar. |

## Expected Final State

All image file types advertise `user_prompt` in metadata; non-image types do not.

## Pass/Fail Criteria

**Pass:**
- `user_prompt` listed for all supported image extensions
- Parameter description is clear and accurate
- Non-image files do not show `user_prompt` or show it as inapplicable

**Fail:**
- `user_prompt` not listed for image files
- Parameter description missing or unclear
- LLM cannot discover the feature via metadata
