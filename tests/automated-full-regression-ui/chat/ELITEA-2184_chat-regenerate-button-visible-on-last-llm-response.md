---
id: ELITEA-2184
title: "Chat – Regenerate Button Visible on Last LLM Response"
priority: high
type: functional
module: chat-interface
status: ready
execution_type: automated
automation_test_id: "tests.ui.chat.test_regenerate_response.TestRegenerateResponse.test_regenerate_visible_only_on_last_response"
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1586
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2184: Chat – Regenerate Button Visible on Last LLM Response

**Module:** chat-interface · **Priority:** high · **Type:** functional

**Objective:** Verify the Regenerate button and action icons are visible only on the last LLM response.

---

## Preconditions

- User is logged in to the Elitea platform.
- A conversation with at least one LLM response exists.

---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Scroll to the last LLM response in the conversation | Last response visible |
| 2 | Hover over the last response | Regenerate button and action icons (speaker, copy, regenerate, delete) visible |
| 3 | Hover over any earlier LLM response | No Regenerate button visible on earlier responses |
| 4 | Verify Regenerate only on last response | Only last response has Regenerate |

---

## Expected Final State

Regenerate is visible only on the last response.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Regenerate visible only on last response.

**Fail:**
- Any step produces an error or unexpected result.
- Regenerate visible on earlier responses or missing on last.
