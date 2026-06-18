---
id: ELITEA-0452
title: "Increasing Steps Limit Allows Previously Failing Multi-Tool Task to Complete"
priority: critical
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:chat, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3292]
---
# ELITEA-0452: Increasing Steps Limit Allows Previously Failing Multi-Tool Task to Complete

**Module:** Chat Interface · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that increasing the Steps Limit from a value that caused early termination allows a task requiring more iterations to complete successfully, confirming the limit is the controlling factor.

**Coverage:**
- Lower limit causes early termination of multi-step task
- Raising the limit allows the same task to run to completion
- Steps Limit is the sole controlling variable between the two outcomes

## Preconditions

- Logged in to {{base_url}}
- Private project selected
- Artifact Toolkit configured with default bucket
- Browser: Chrome (latest)

## Test Data

- First Steps Limit: 3
- Second Steps Limit: 15
- Prompt: "list files from folder 5 times: after each listing find the file with the lowest size, if no files just proceed. Details: default bucket, recursive, analyze after each listing, then proceed without approval"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open a conversation with Artifact Toolkit added. Set Steps Limit to '3' via Model Settings. Send the prompt. | Execution stops at 3 iterations with message 'Maximum tool execution iterations (3) reached. Stopping tool execution.' |
| 2 | Open Model Settings again. Change Steps Limit to '15'. Click Apply. | Modal closes. Steps Limit updated to 15. |
| 3 | Send the same prompt again. | The AI executes all 5 listing operations without hitting a steps limit error. |
| 4 | Confirm no 'Maximum tool execution iterations' error appears in the response. | All 5 iterations complete. Response shows analysis results for each listing. No iteration limit error. |

## Expected Final State

All 5 iterations complete. Response shows analysis results for each listing. No iteration limit error.

## Pass/Fail Criteria

**Pass:**
- With limit 3: execution stops at 3 iterations with correct error message
- With limit 15: all 5 listing operations complete without a steps limit error

**Fail:**
- With limit 3: execution completes all 5 iterations (limit not enforced)
- With limit 15: execution still terminates early with a steps limit error
- Any unexpected crash or freeze occurs
