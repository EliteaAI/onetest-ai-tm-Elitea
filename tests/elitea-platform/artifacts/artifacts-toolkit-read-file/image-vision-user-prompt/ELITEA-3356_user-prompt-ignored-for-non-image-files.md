---
id: ELITEA-3356
title: "user_prompt Ignored for Non-Image Files (TXT, PDF)"
priority: critical
type: functional
module: artifacts-toolkit-read-file
status: draft
execution_type: manual
tags: [feat:artifacts, feat:image-vision, r-2.0.6, parameter-isolation]
requirements: [EliteaAI/elitea_issues#6530]
---
# ELITEA-3356: user_prompt Ignored for Non-Image Files (TXT, PDF)

**Module:** Artifacts Toolkit Read File · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that `read_file` with `extra_params={"user_prompt": "..."}` for non-image files (TXT, PDF) ignores the parameter and reads the file normally.

**Coverage:**
- `user_prompt` parameter isolation to image files only
- No errors when `user_prompt` passed for non-image files
- Normal file reading behavior preserved

## Preconditions

- Logged in to dev environment
- Artifact Toolkit with `read_file` enabled
- `test_document.txt` with known text content in bucket `test`
- `test_document.pdf` with known text content in bucket `test`

## Test Data

| File | Content | extra_params |
|---|---|---|
| test_document.txt | "Hello World content" | {"user_prompt": "Summarize this in 5 words"} |
| test_document.pdf | Multi-page document | {"user_prompt": "What is on page 2?"} |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call `read_file` on `test_document.txt` with `extra_params={"user_prompt": "Summarize this in 5 words"}`. | Tool executes successfully. Full text content returned. |
| 2 | Verify the TXT file content is returned as-is. | Response contains "Hello World content" — the raw file content, not a 5-word summary. |
| 3 | Call `read_file` on `test_document.pdf` with `extra_params={"user_prompt": "What is on page 2?"}`. | Tool executes successfully. PDF content returned normally. |
| 4 | Verify PDF is processed using standard PDF reading, not vision. | PDF text is extracted normally; `user_prompt` does not affect behavior. |

## Expected Final State

Non-image files are read normally; `user_prompt` parameter is silently ignored without errors.

## Pass/Fail Criteria

**Pass:**
- TXT file returns raw content
- PDF file returns extracted text
- No errors when `user_prompt` passed for non-image files
- `user_prompt` has no effect on non-image processing

**Fail:**
- Error returned when `user_prompt` used with non-image files
- Non-image file processing affected by `user_prompt`
- Parameter leaks to non-image loaders causing unexpected behavior
