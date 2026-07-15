---
id: ELITEA-2186
title: "Chat – Regenerate After Stopped Generation Produces New Output"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2186: Chat – Regenerate After Stopped Generation Produces New Output

**Module:** chat-interface · **Priority:** high · **Type:** functional

**Objective:** Verify that clicking Regenerate after a stopped generation produces a new complete response.

---

## Preconditions

- User is logged in to the Elitea platform.
- A conversation where a previous generation was stopped exists.

---

## Test Data

| Field | Value |
|-------|-------|
| Message | generate a poem |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Type 'generate a poem' and click Send; click stop to cancel mid-stream | Generation stopped; partial or no content in response |
| 2 | Hover over the stopped response and click Regenerate | New generation begins |
| 3 | Verify orange stop button appears during regeneration | Stop button visible |
| 4 | Wait for new response to complete | Full response generated |
| 5 | Verify Regenerate and action icons reappear; user message unchanged | Actions visible; user message unchanged |

---

## Expected Final State

Regenerate after stop produces a new complete response.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Regenerate after stop works.

**Fail:**
- Any step produces an error or unexpected result.
- Regenerate fails after stopped generation.
