---
id: ELITEA-2616
title: "Chat – Stop Button Visible Only During Thinking/Sub-Agent Phase, Hidden Once Response Streaming Starts"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat, issue:5196]
requirements: [EliteaAI/elitea_issues#5196]
---

# ELITEA-2616: Chat – Stop Button Visible Only During Thinking/Sub-Agent Phase, Hidden Once Response Streaming Starts

**Module:** chat-interface · **Priority:** High · **Type:** Functional

**Objective:** Verify the Stop button is available while sub-agents/tools are working ("thinking" steps), and becomes unavailable once actual response text has begun streaming — since at that point there is nothing left to interrupt.

---

## Preconditions

- User is logged in to the Elitea platform.
- User has an open conversation with an agent that performs visible "thinking"/tool-call steps before producing a final response (e.g. an agent with a toolkit attached).

---

## Test Data

| Field | Value |
|-------|-------|
| Message | A prompt that triggers a tool call / sub-agent step before the final answer (e.g. "search Jira for open bugs and summarize") |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Send the message and observe the "thinking"/tool-call steps appearing | Thinking/sub-agent steps are shown; Stop button is visible on the input bar |
| 2 | Keep observing without clicking Stop, until the model begins streaming the final response text | Once response text streaming begins, verify whether Stop button is still shown |
| 3 | Confirm expected behavior: Stop should be hidden/disabled once streaming of the final answer starts (nothing left to interrupt) | Stop button hidden/disabled; Send button state restored or response completes normally |

---

## Expected Final State

Stop button is present only during the "thinking"/sub-agent phase; once the final response begins streaming, the Stop control is no longer available.

---

## Pass/Fail Criteria

**Pass:**
- Stop button is visible during thinking/sub-agent execution.
- Stop button is hidden/disabled once final response text streaming has started.

**Fail:**
- Stop button remains visible/clickable after streaming of the final response has begun.
- Stop button is missing during the thinking/sub-agent phase.
