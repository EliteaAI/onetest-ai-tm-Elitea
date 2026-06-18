---
id: ELITEA-0489
title: "Verify Attachment Button Disabled When Backend Returns No Code Types"
priority: high
type: functional
module: chat-interface
status: ready
execution_type: manual
tags: [programming-files, feat:attachments, error-handling, regression, story:3671, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3671]
---
# ELITEA-0489: Verify Attachment Button Disabled When Backend Returns No Code Types

**Module:** Chat Interface · **Priority:** High · **Type:** Functional

**Objective:** Verify that the attachment button remains disabled (no file types available) if the backend API returns an empty or missing `code_types` field AND also returns no `document_types` or `image_types`. This tests the "no fallback" behavior established in the Redux slice — the UI should not permit attachments if the API provides no file type data.

## Preconditions

1. User is logged into Elitea platform
2. A Chat conversation is open
3. The backend API for the project's `/index_types/prompt_lib/{projectId}` returns an empty response `{}` or a response where `document_types`, `image_types`, and `code_types` are all absent/empty
4. This can be simulated via a test project configuration or by mocking the API response

## Test Data

- Mock/test project where document loaders API returns `{}` or `{"document_types": {}, "image_types": {}, "code_types": {}}`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open a Chat conversation in the project where the API returns no file type data | Conversation is displayed |
| 2 | Observe the attachment (paperclip) button state | The attachment button is visually disabled (grayed out or has a disabled appearance) |
| 3 | Hover over the disabled attachment button | Tooltip may indicate why it is disabled (e.g., "Loading..." or "No file types available") |
| 4 | Attempt to click the disabled attachment button | No file picker dialog opens; button does not respond to clicks |

## Expected Final State

No file picker dialog opens; button does not respond to clicks

## Pass/Fail Criteria

- PASS: Attachment button is disabled when `allowedExtensions` array is empty (from Redux state); button does not open file picker when clicked in disabled state
- FAIL: Attachment button is enabled despite no file types being available from the API; file picker opens with no restrictions; any crash or unhandled error
