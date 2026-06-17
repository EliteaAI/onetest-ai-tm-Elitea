---
id: ELITEA-0299
title: "Mixed Session – Text and Image Files Read in Same Conversation"
priority: high
type: functional
module: artifacts
status: ready
execution_type: manual
tags: [feat:artifacts, eng:api, r-2.0.1, bug]
requirements: [ProjectAlita/projectalita.github.io#3644]
---
# ELITEA-0299: Mixed Session – Text and Image Files Read in Same Conversation

**Module:** Artifacts · **Priority:** High · **Type:** Functional

**Objective:** Verify that within a single Chat conversation, an agent can sequentially read a text artifact file and then an image artifact file in the same session using Claude Sonnet 4.6 and Claude Sonnet 4.5 without state or context errors.

**Coverage:**
- Text and image file reads co-exist in same conversation session with Claude 4.6
- Text and image file reads co-exist in same conversation session with Claude 4.5
- No context contamination or errors when switching file types within one session

## Preconditions

- Logged in to {{base_url}}
- An Artifact bucket contains both notes.txt (with sample text) and photo.png (any image)
- A Chat conversation with the Artifact Toolkit is configured
- Claude Sonnet 4.6 and 4.5 are available

## Test Data

- Bucket files: notes.txt (sample text content), photo.png (any image)
- LLM pass 1: Claude Sonnet 4.6
- LLM pass 2: Claude Sonnet 4.5

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chat and open a conversation with Artifact Toolkit attached. Set LLM to Claude Sonnet 4.6. | Conversation is active with Claude Sonnet 4.6. |
| 2 | Send: 'Read notes.txt from the bucket and summarize it.' | Agent reads notes.txt and returns a summary without errors. |
| 3 | Send: 'Now read photo.png from the bucket and describe it.' | Agent reads photo.png and returns a description without errors in the same session. |
| 4 | Start a new conversation and set LLM to Claude Sonnet 4.5. | New conversation is active with Claude Sonnet 4.5. |
| 5 | Repeat steps 2–3 in the new conversation. | Both files are read successfully with Claude Sonnet 4.5 in a mixed-type session. |

## Expected Final State

Both files are read successfully with Claude Sonnet 4.5 in a mixed-type session.

## Pass/Fail Criteria

**Pass:**
- Text file is read and summarized correctly
- Image file is read and described correctly in the same session
- No errors occur on either read for both Claude versions

**Fail:**
- Reading image after text (or vice versa) causes an InternalSDKError
- Any file read fails in mixed-type session context
