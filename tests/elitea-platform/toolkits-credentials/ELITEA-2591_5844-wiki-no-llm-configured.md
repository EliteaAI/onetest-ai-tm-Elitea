---
id: ELITEA-2591
title: "[EliteaAI/elitea_issues#5844] ADO Wiki: No LLM Configured (Graceful Fallback)"
priority: high
type: functional
module: toolkits-credentials
status: ready
execution_type: manual
tags: [issue:5844, r-2.0.5, feat:toolkits, int:ado-boards, eng:ai, eng:backend, caching]
requirements: [EliteaAI/elitea_issues#5844]
---

# ELITEA-2591: ADO Wiki — No LLM Configured (Graceful Fallback)

**Module:** Toolkits Credentials · **Priority:** High · **Type:** Functional

**Objective:** Verify graceful fallback when LLM is not configured but image processing is requested.

## Preconditions

- ADO toolkit configured with `process_images: true`
- `image_description_prompt` is set
- Wiki page contains images
- LLM is NOT configured or not accessible
- Tool/agent logs visible

## Test Data

| Config | Value |
|--------|-------|
| process_images | true |
| image_description_prompt | Set |
| LLM configured | false |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Run wiki page retrieval with `process_images=true` and prompt set, but NO LLM. | Tool processes page. |
| 2 | Verify existing error/fallback behavior remains unchanged. | Behavior consistent with prior toolkit behavior (before enhancement). |
| 3 | Check for crash or exception. | No crash; tool completes. |
| 4 | Verify clear error or skip behavior. | Clear error message or images skipped gracefully. |
| 5 | Check wiki page content is still returned. | Page content available (with or without image descriptions). |
| 6 | Verify error message is descriptive. | User understands LLM not configured (if error approach). |
| 7 | Confirm no data corruption or invalid content. | Page content remains valid. |

## Expected Final State

- No crash when LLM unavailable
- Clear error or skip behavior (consistent with pre-feature behavior)
- Wiki page content still returned
- Descriptive error message if applicable
- No data corruption

## Pass/Fail Criteria

**Pass:** No crash; clear behavior; content returned; consistent with prior fallback.  
**Fail:** Crash/exception; unclear error; missing content; different fallback behavior.
