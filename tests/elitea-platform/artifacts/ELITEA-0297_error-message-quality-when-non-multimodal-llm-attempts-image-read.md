---
id: ELITEA-0297
title: "Error Message Quality When Non-Multimodal LLM Attempts Image Read"
priority: medium
type: functional
module: artifacts
status: ready
execution_type: manual
tags: [feat:artifacts, eng:api, r-2.0.1, bug]
requirements: [ProjectAlita/projectalita.github.io#3644]
---
# ELITEA-0297: Error Message Quality When Non-Multimodal LLM Attempts Image Read

**Module:** Artifacts · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that when a non-multimodal LLM attempts to read an image from an artifact, the error message shown in the Chat UI is informative and does not expose raw internal stack traces.

**Coverage:**
- Non-multimodal LLM image read produces a user-friendly error message
- Raw Python tracebacks or internal SDK error details are not exposed in the chat UI

## Preconditions

- Logged in to {{base_url}}
- A non-multimodal (text-only) LLM model is available and selectable in the conversation
- An Artifact Toolkit is configured with a bucket containing an image file
- A Chat conversation with the Artifact Toolkit is set up

## Test Data

- LLM: any text-only non-multimodal model available in the project
- Image filename: image.png
- Bucket: any bucket containing image.png

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chat and open a conversation with the Artifact Toolkit attached. | Conversation is active. |
| 2 | Set the LLM to a non-multimodal text-only model. | A text-only LLM is selected. |
| 3 | Send: 'Read image.png from the bucket and describe it.' | Agent attempts to invoke readFile. |
| 4 | Observe the response in the Chat UI. | A user-friendly error message is displayed. No raw Python traceback, no litellm error stack, no InternalSDKError text is visible to the end user. |

## Expected Final State

A user-friendly error message is displayed. No raw Python traceback, no litellm error stack, no InternalSDKError text is visible to the end user.

## Pass/Fail Criteria

**Pass:**
- A clear, human-readable error or limitation message is shown (e.g., 'This model does not support image reading')
- No raw Python traceback or SDK internal error text is visible in the chat

**Fail:**
- Raw InternalSDKError stack trace text is displayed to the user in the chat response
- No error message is shown at all (silent failure)
