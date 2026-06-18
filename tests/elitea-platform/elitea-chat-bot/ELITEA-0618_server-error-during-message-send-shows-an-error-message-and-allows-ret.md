---
id: ELITEA-0618
title: "Server error during message send shows an error message and allows retry"
priority: high
type: functional
module: elitea-chat-bot
status: draft
execution_type: manual
tags: [error-handling, network-error, story:4775, r-2.0.3, retry]
requirements: [4775]
---
# ELITEA-0618: Server error during message send shows an error message and allows retry

**Module:** Elitea Chat Bot · **Priority:** High · **Type:** Functional

**Objective:** Verify that if the server returns an error (e.g., 500 or timeout) while processing a user message, the Support Assistant shows a user-friendly error notification in the panel — not a blank screen, not a silent failure. The user must be able to retry the message.

## Preconditions

Support Assistant is enabled.
The tester can simulate a server error (e.g., by temporarily disabling the backend, using a network throttle, or using a pre-configured error agent). If simulation is not possible in the test environment, this test may require coordination with the dev team to trigger the error condition.

## Test Data

Any test message (e.g., "Hello")
Backend configured to return 500 for this test

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the Support Assistant panel | Panel opens normally |
| 2 | Send a message while the server is configured to return a 500 error | The loading indicator appears briefly |
| 3 | Observe the panel after the error | An error message or toast is displayed in the panel (e.g., "Something went wrong, please try again") — NOT a blank or frozen panel |
| 4 | Check whether a retry mechanism is available | A "Retry" button or instruction is visible |
| 5 | Restore the backend to normal operation and click Retry | Message is resent; a valid assistant response is received |

## Expected Final State

Message is resent; a valid assistant response is received

## Pass/Fail Criteria

PASS: Error message shown in panel; retry works; no blank/frozen panel state.
FAIL: Panel goes blank or shows raw error code; no retry option; panel becomes unusable.
