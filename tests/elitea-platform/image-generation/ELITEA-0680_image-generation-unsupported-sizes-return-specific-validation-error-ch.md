---
id: ELITEA-0680
title: "Image Generation — Unsupported Sizes Return Specific Validation Error [Chat & Agent]"
priority: high
type: functional
module: image-generation
status: ready
execution_type: manual
tags: [feat:image-generation, nfr:validation, eng:backend, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#4010]
---
# ELITEA-0680: Image Generation — Unsupported Sizes Return Specific Validation Error [Chat & Agent]

**Module:** Image Generation · **Priority:** High · **Type:** Functional

**Objective:** Verify that requesting image generation with an unsupported size (too small or too large) returns a specific validation error naming the invalid value and listing supported sizes — tested from both Chat and Agent.

**Coverage:**
- Unsupported sizes below minimum (256x256, 512x512) — Chat
- Unsupported sizes above maximum (2048x2048, 2048x1024) — Chat
- Unsupported sizes (256x256, 512x512) — Agent
- Error message names the invalid value and lists all supported sizes explicitly
- Regression: all supported sizes (1024x1024, 1024x1536, 1536x1024, auto) generate successfully

## Preconditions

- Logged in to {{base_url}}
- Chat session with an image generation model configured (e.g., DALL-E or equivalent)
- Agent with image generation capability enabled
- Browser: Chrome (latest stable)

## Test Data

| Entry Point | Size     | Prompt             | Expected          |
|-------------|----------|--------------------|-------------------|
| Chat        | 256x256  | A medieval castle  | Specific error    |
| Chat        | 512x512  | A medieval castle  | Specific error    |
| Chat        | 2048x2048| A medieval castle  | Specific error    |
| Chat        | 2048x1024| A medieval castle  | Specific error    |
| Chat        | 1024x1024| A medieval castle  | Image generated   |
| Chat        | 1024x1536| A medieval castle  | Image generated   |
| Chat        | 1536x1024| A medieval castle  | Image generated   |
| Chat        | auto     | A medieval castle  | Image generated   |
| Agent       | 256x256  | A medieval castle  | Specific error    |
| Agent       | 512x512  | A medieval castle  | Specific error    |
| Agent       | 1024x1024| A medieval castle  | Image generated   |

Expected error format: {"message": "Error: Image generation failed (400): Invalid value: '<size>'. Supported values are: '1024x1024', '1024x1536', '1536x1024', and 'auto'."}

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Chat with an image generation model active. | Chat session is ready. |
| 2 | Request image generation with size 256x256 and prompt 'A medieval castle'. | Error returned: "Error: Image generation failed (400): Invalid value: '256x256'. Supported values are: '1024x1024', '1024x1536', '1536x1024', and 'auto'." |
| 3 | Repeat with size 512x512. | Same structured error, referencing '512x512' as the invalid value. |
| 4 | Repeat with size 2048x2048. | Same structured error, referencing '2048x2048' as the invalid value. |
| 5 | Repeat with size 2048x1024. | Same structured error, referencing '2048x1024' as the invalid value. |
| 6 | Request with size 1024x1024 and prompt 'A medieval castle'. | Image generated successfully, no error. |
| 7 | Request with size 1024x1536. | Image generated successfully, no error. |
| 8 | Request with size 1536x1024. | Image generated successfully, no error. |
| 9 | Request with size auto. | Image generated successfully, no error. |
| 10 | Open an Agent with image generation enabled. | Agent chat interface is ready. |
| 11 | Request image generation with size 256x256 and prompt 'A medieval castle'. | Same structured error as step 2. |
| 12 | Repeat with size 512x512. | Same structured error, referencing '512x512'. |
| 13 | Request with size 1024x1024 and prompt 'A medieval castle'. | Image generated successfully (regression check). |

## Expected Final State

Image generated successfully (regression check).

## Pass/Fail Criteria

**Pass:**
- All unsupported sizes return: "Error: Image generation failed (400): Invalid value: '<size>'. Supported values are: '1024x1024', '1024x1536', '1536x1024', and 'auto'." — from both Chat and Agent
- The invalid size value is correctly named in the error message
- All supported sizes (1024x1024, 1024x1536, 1536x1024, auto) generate images without error

**Fail:**
- Any unsupported size returns a generic "400 Bad Request" or "Unexpected error" without naming the invalid value or listing supported values
- Any supported size fails to generate an image (regression)
- Error message omits the invalid value or supported values list
- Chat and Agent behave differently for the same size
