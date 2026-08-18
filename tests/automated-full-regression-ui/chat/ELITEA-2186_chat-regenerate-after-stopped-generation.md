---
id: ELITEA-2186
title: "Chat – Regenerate After Stopped Generation Produces New Output"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat, issue:5196]
requirements: [EliteaAI/elitea_issues#5196]
---

# ELITEA-2186: Chat – Regenerate After Stopped Generation (Mid-Stream) Produces New Output

**Module:** chat-interface · **Priority:** high · **Type:** functional

**Objective:** Verify that clicking Regenerate after a generation is stopped **mid-stream (with partial response text already visible)** produces a new complete response. This scenario is now distinct from stopping during the thinking/sub-agent phase (see ELITEA-2618), where the exchange is removed entirely and there is no message left to regenerate.

**Important scope note (per issue #5196 implementation):** the backend only preserves a message to regenerate/salvage when there is actual content — either streamed response text or a salvageable "thinking step" text. If the stop happens before any content exists at all, both the user and assistant message are deleted and no Regenerate action is available (covered by ELITEA-2618). This test specifically covers the case where partial content DOES exist at the time of stop.

---

## Preconditions

- User is logged in to the Elitea platform.
- User has an open conversation with an agent whose response streams visibly (so a stop can be timed to occur after some text has already appeared).

---

## Test Data

| Field | Value |
|-------|-------|
| Message | generate a long detailed poem about the seasons |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Type the message and click Send; wait until response text has started streaming and some visible content exists, then click Stop | Generation stopped; partial response text is preserved and visible in the chat (message is NOT deleted, since content exists) |
| 2 | Hover over the stopped response and verify a Regenerate action is available | Regenerate icon visible on the partial response |
| 3 | Click Regenerate | New generation begins |
| 4 | Verify stop button appears during regeneration | Stop button visible |
| 5 | Wait for new response to complete | Full response generated |
| 6 | Verify Regenerate and action icons reappear; user message unchanged | Actions visible; user message unchanged |

---

## Expected Final State

Regenerate after a mid-stream stop (with partial content already present) produces a new complete response, replacing the partial one.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Partial content is preserved (not deleted) since it existed before stop.
- Regenerate after stop works and produces a full new response.

**Fail:**
- Any step produces an error or unexpected result.
- Partial content is unexpectedly deleted despite existing before stop.
- Regenerate fails after stopped generation.
