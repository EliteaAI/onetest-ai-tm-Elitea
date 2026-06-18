---
id: ELITEA-0620
title: "Assistant response streams in real time token by token"
priority: high
type: functional
module: elitea-chat-bot
status: ready
execution_type: manual
tags: [response-rendering, story:4775, real-time, streaming, r-2.0.3]
requirements: [4775]
---
# ELITEA-0620: Assistant response streams in real time token by token

**Module:** Elitea Chat Bot · **Priority:** High · **Type:** Functional

**Objective:** Verify that when the assistant is generating a response, the text appears progressively (token-by-token or chunk-by-chunk) in the conversation area rather than appearing all at once after a delay. This confirms streaming is enabled end-to-end. Also confirms the input composer is disabled during streaming and re-enabled once streaming completes.

## Preconditions

Support Assistant is enabled with a streaming-capable Agent configured.
Tester is logged in as a regular user with the Support Assistant panel open.

## Test Data

Message that produces a multi-sentence response: "Give me step-by-step instructions for creating a new agent in ELITEA"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Type the test message and send it | Message appears in the conversation area |
| 2 | Observe the assistant response area immediately after sending | A loading or "thinking" indicator appears |
| 3 | Watch the response area while the assistant generates | Text appears incrementally — partial words or sentences become visible progressively, not all at once |
| 4 | Verify the message input field state during response generation | Input field is disabled or shows a visual indicator that it is locked; Send button is inactive |
| 5 | Wait for the full response to complete | Complete response is displayed; input field becomes active again |

## Expected Final State

Complete response is displayed; input field becomes active again

## Pass/Fail Criteria

PASS: Text streams incrementally; input locked during generation; input enabled after completion.
FAIL: Response appears all at once with no streaming; input remains enabled during generation (allows double-send).
