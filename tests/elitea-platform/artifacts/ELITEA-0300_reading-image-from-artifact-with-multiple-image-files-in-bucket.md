---
id: ELITEA-0300
title: "Reading Image from Artifact with Multiple Image Files in Bucket"
priority: high
type: functional
module: artifacts
status: ready
execution_type: manual
tags: [feat:artifacts, eng:api, r-2.0.1, bug]
requirements: [ProjectAlita/projectalita.github.io#3644]
---
# ELITEA-0300: Reading Image from Artifact with Multiple Image Files in Bucket

**Module:** Artifacts · **Priority:** High · **Type:** Functional

**Objective:** Verify that when a bucket contains multiple image files, the agent can read a specific image by filename using Claude Sonnet 4.6 and Claude Sonnet 4.5 without errors.

**Coverage:**
- Agent correctly reads each of 3+ image files in different formats from a bucket using Claude 4.6
- Agent correctly reads each of 3+ image files in different formats from a bucket using Claude 4.5
- No cross-file contamination or errors when issuing sequential readFile calls in one conversation

## Preconditions

- Logged in to {{base_url}}
- An Artifact bucket contains at least 3 image files of different formats: img1.png, img2.jpg, img3.webp
- A Chat conversation is configured with the Artifact Toolkit
- Claude Sonnet 4.6 and 4.5 are both available

## Test Data

- Bucket files: img1.png, img2.jpg, img3.webp
- LLM pass 1: Claude Sonnet 4.6
- LLM pass 2: Claude Sonnet 4.5

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chat and open a conversation with the Artifact Toolkit attached. | Conversation is active with Artifact Toolkit as participant. |
| 2 | Set LLM to Claude Sonnet 4.6. | Claude Sonnet 4.6 is active. |
| 3 | Send: 'Read img1.png from the bucket and describe it.' | Agent reads img1.png and returns a description without errors. |
| 4 | Send: 'Read img2.jpg from the bucket and describe it.' | Agent reads img2.jpg and returns a description without errors. |
| 5 | Send: 'Read img3.webp from the bucket and describe it.' | Agent reads img3.webp and returns a description without errors. |
| 6 | Repeat steps 2–5 for a new conversation with LLM set to Claude Sonnet 4.5. | All three images are read successfully with Claude Sonnet 4.5 as well. |

## Expected Final State

All three images are read successfully with Claude Sonnet 4.5 as well.

## Pass/Fail Criteria

**Pass:**
- Each image file read returns a relevant description
- No errors across all 3 file reads for both Claude versions

**Fail:**
- Any readFile call results in an InternalSDKError
- Agent returns wrong file content or confuses file identities
- Error occurs on second or third image read after first succeeds
