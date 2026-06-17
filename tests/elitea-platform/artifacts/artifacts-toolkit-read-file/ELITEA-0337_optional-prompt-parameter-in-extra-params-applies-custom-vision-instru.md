---
id: ELITEA-0337
title: "Optional prompt Parameter in extra_params Applies Custom Vision Instruction"
priority: medium
type: functional
module: artifacts-toolkit-read-file
status: draft
execution_type: manual
tags: [feat:attachments, feat:artifacts, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4629]
---
# ELITEA-0337: Optional prompt Parameter in extra_params Applies Custom Vision Instruction

**Module:** Artifacts Toolkit Read File · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that a custom `prompt` key in `extra_params` shapes the vision model's transcription output differently from the default prompt.

**Coverage:**
- `prompt` parameter accepted inside `extra_params` JSON string
- Custom prompt output differs from default prompt output
- Default behavior preserved when `prompt` is omitted

## Preconditions

- Logged in to dev environment
- Artifact Toolkit with `readFile` enabled; multimodal LLM configured
- `docx_with_images.docx` in bucket `test`

## Test Data

| Scenario | extra_params |
|---|---|
| Custom prompt | {\"prompt\": \"List only the text visible in this image as a bulleted list.\"} |
| No prompt (default) | {} or omitted |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call `readFile` on `docx_with_images.docx` with `is_capture_image=True` and `extra_params` = `{"prompt": "List only the text visible in this image as a bulleted list."}` as a JSON string. | Tool executes. Response returned with image transcription. |
| 2 | Note the transcription format and content. | Transcription is formatted as a bulleted list of visible text, as instructed by the custom prompt. |
| 3 | Call `readFile` on the same file with `is_capture_image=True` but without a `prompt` in `extra_params` (or omit `extra_params` entirely). | Tool executes. Response returned with image transcription using the default prompt. |
| 4 | Compare the two responses. | The custom-prompt response follows the specified format. The default-prompt response uses the standard description format. The two responses differ clearly. |

## Expected Final State

The custom-prompt response follows the specified format. The default-prompt response uses the standard description format. The two responses differ clearly.

## Pass/Fail Criteria

**Pass:**
- Custom prompt output matches the specified format
- Default prompt produces different output
- No errors on `prompt` key in `extra_params`

**Fail:**
- Both responses identical regardless of prompt
- Custom prompt ignored
- Error returned when `prompt` key is present in `extra_params`
