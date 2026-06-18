---
id: ELITEA-0305
title: "Image from Artifact Read Successfully in Chat – Claude Sonnet 4.6"
priority: critical
type: functional
module: artifacts
status: ready
execution_type: manual
tags: [feat:artifacts, eng:api, r-2.0.1, bug]
requirements: [ProjectAlita/projectalita.github.io#3644]
---
# ELITEA-0305: Image from Artifact Read Successfully in Chat – Claude Sonnet 4.6

**Module:** Artifacts · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that a user can ask the agent to read an image from an artifact bucket in a Chat conversation using Claude Sonnet 4.6 without receiving a 'thinking' tag mismatch 400 error.

**Coverage:**
- readFile tool call on an image succeeds with Claude Sonnet 4.6
- No InternalSDKError with 'thinking' tag mismatch is thrown
- Agent returns a description of the image content

## Preconditions

- Logged in to {{base_url}}
- An Artifact Toolkit is configured with a bucket containing at least one image file (e.g., sample.png)
- A Chat conversation exists (or can be created) with the Artifact Toolkit added as a participant
- Claude Sonnet 4.6 is available as an LLM option in the project

## Test Data

- Bucket name: any bucket with an image file
- Image filename: sample.png (or any .jpg/.jpeg/.png/.webp)
- LLM: Claude Sonnet 4.6
- URL: {{base_url}}

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chat from the sidebar. | Chat page loads and the conversation list is visible. |
| 2 | Open an existing conversation or create a new one by clicking +Create. | Conversation editor opens. |
| 3 | In the Participants section, add the configured Artifact Toolkit. | Artifact Toolkit appears in the participants list. |
| 4 | Set the LLM model to Claude Sonnet 4.6. | Claude Sonnet 4.6 is selected as the active model. |
| 5 | Send the message: 'Read the image sample.png from the bucket and describe what you see.' | The agent executes the readFile tool call without errors. |
| 6 | Observe the agent's response in the chat. | Agent returns a textual description of the image. No error message, no InternalSDKError, no 'thinking tag mismatch' error is shown. |

## Expected Final State

Agent returns a textual description of the image. No error message, no InternalSDKError, no 'thinking tag mismatch' error is shown.

## Pass/Fail Criteria

**Pass:**
- Agent successfully reads the image and returns a description
- No 400 or 500 error is thrown
- No 'thinking' tag mismatch error appears in the response

**Fail:**
- InternalSDKError with status 400 and 'thinking' tag message is raised
- Chat shows an error response instead of image description
- Agent execution fails or times out
