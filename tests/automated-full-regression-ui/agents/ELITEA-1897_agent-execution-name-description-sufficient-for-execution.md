---
id: ELITEA-1897
title: "Agent execution — instructions field alone does not prevent execution (name+description sufficient)"
priority: high
type: functional
module: agents
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:agents]
requirements: []
---

# ELITEA-1897: Agent execution — instructions field alone does not prevent execution (name+description sufficient)

**Module:** agents · **Priority:** high · **Type:** functional

**Objective:** Verify that an agent with Name, Description, and Instructions can be executed from the embedded chat panel and responds correctly without hanging indefinitely.

---

## Preconditions

- User is logged in to the Elitea platform.

---

## Test Data

| Field | Value |
|-------|-------|
| Test message | Reply with: CONFIRMED |
| Expected response | CONFIRMED |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create an agent with Name, Description, and Instructions filled | The agent is created successfully |
| 2 | In the embedded chat panel, send the message "Reply with: CONFIRMED" | The message is submitted to the chat |
| 3 | Verify the agent responds with a message containing "CONFIRMED" | The agent response contains "CONFIRMED" |
| 4 | Verify no error state or "waking the agent" spinner hangs indefinitely | No persistent loading spinner or error state is shown |

---

## Expected Final State

The agent responds with "CONFIRMED" in the embedded chat panel without any error or indefinite loading state.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The agent responds with "CONFIRMED" and no spinner hangs indefinitely.

**Fail:**
- Any step produces an error or unexpected result.
- No response is received, the spinner hangs indefinitely, or an error state is shown.
