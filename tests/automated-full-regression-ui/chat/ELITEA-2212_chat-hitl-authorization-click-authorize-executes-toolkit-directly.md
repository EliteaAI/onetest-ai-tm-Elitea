---
id: ELITEA-2212
title: "Chat – HITL Authorization – Click Authorize Button and Verify Toolkit Tool Executes Directly"
priority: high
type: functional
module: chat-interface
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:chat]
requirements: []
automation_test_id: tests.ui.chat.test_hitl_sensitive_action_authorization.TestSensitiveActionAuthorize.test_authorize_executes_toolkit_tool_directly
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1836
automation_known_defect: "#1834, #1835"
---

# ELITEA-2212: Chat – HITL Authorization – Click Authorize Button and Verify Toolkit Tool Executes Directly

**Module:** chat-interface · **Priority:** high · **Type:** functional

**Objective:** Verify that clicking Authorize allows the toolkit to execute the sensitive action directly.

---

## Preconditions

- User is logged in to the Elitea platform.
- HITL authorization card is showing for a sensitive toolkit action.

---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Verify HITL authorization card shows with Authorize/Block/Block with Comment buttons | Cards and buttons visible |
| 2 | Click 'Authorize' (green with checkmark) | Authorization card closes; toolkit proceeds to execute |
| 3 | Verify tool execution completes successfully | Execution completes |
| 4 | Verify tool execution chips shown: LLM model and toolkit tool chips | Chips visible |
| 5 | Verify conversation continues normally | No errors |

---

## Expected Final State

Toolkit executes after authorization; chips shown.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Authorize allows toolkit execution.

**Fail:**
- Any step produces an error or unexpected result.
- Authorize does not execute toolkit.
