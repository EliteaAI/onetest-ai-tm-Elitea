---
id: ELITEA-3359
title: "Invalid JSON in extra_params Returns Clear Error"
priority: critical
type: negative
module: artifacts-toolkit-read-file
status: draft
execution_type: manual
tags: [feat:artifacts, feat:image-vision, r-2.0.6, error-handling]
requirements: [EliteaAI/elitea_issues#6530]
---
# ELITEA-3359: Invalid JSON in extra_params Returns Clear Error

**Module:** Artifacts Toolkit Read File · **Priority:** Critical · **Type:** Negative

**Objective:** Verify that `extra_params` with invalid JSON returns a clear, actionable error message without crashing the tool.

**Coverage:**
- Graceful error handling for malformed JSON
- Clear error message for developers
- No tool crash or hang

## Preconditions

- Logged in to dev environment
- Artifact Toolkit with `read_file` enabled
- `test_image.png` in bucket `test`

## Test Data

| Scenario | extra_params (invalid) |
|---|---|
| Missing closing brace | {"user_prompt": "test" |
| Single quotes | {'user_prompt': 'test'} |
| Unquoted key | {user_prompt: "test"} |
| Trailing comma | {"user_prompt": "test",} |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call `read_file` on `test_image.png` with `extra_params` = `{"user_prompt": "test"` (missing closing brace). | Error returned with clear JSON parsing message. |
| 2 | Verify error message is actionable. | Message indicates "Invalid JSON" or "JSON parsing error" with position or hint. |
| 3 | Test with single quotes: `{'user_prompt': 'test'}`. | Similar clear error about JSON format. |
| 4 | Test with unquoted key: `{user_prompt: "test"}`. | Clear error returned. |
| 5 | Verify no tool crash or hang in any scenario. | All errors return gracefully without requiring session restart. |

## Expected Final State

Clear, actionable error messages for all invalid JSON scenarios; tool remains functional.

## Pass/Fail Criteria

**Pass:**
- All invalid JSON scenarios return clear errors
- Error messages help identify the issue
- Tool does not crash or hang

**Fail:**
- Tool crashes on invalid JSON
- Cryptic or unhelpful error message
- Tool hangs indefinitely
