---
id: ELITEA-2214
title: "Chat – HITL Authorization – Click Block with Comment Button for Direct Toolkit Call"
priority: high
type: functional
module: chat-interface
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:chat]
requirements: []
automation_test_id: tests.ui.chat.test_hitl_sensitive_action_authorization.TestSensitiveActionBlockWithComment.test_block_with_comment_records_reason_and_blocks_action
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1843
automation_known_defect: "#1834, #1835"
---

# ELITEA-2214: Chat – HITL Authorization – Click Block with Comment Button for Direct Toolkit Call

**Module:** chat-interface · **Priority:** high · **Type:** functional

**Objective:** Verify that clicking 'Block with Comment' prompts for a comment and blocks the toolkit action after submission.

---

## Preconditions

- User is logged in to the Elitea platform.
- HITL authorization card is showing for a sensitive toolkit action.

---

## Test Data

| Field | Value |
|-------|-------|
| Block comment | This action is too risky and could delete important data |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Click 'Block with Comment' (gray with comment icon) | Modal/text input appears for blocking reason |
| 2 | Type comment: 'This action is too risky and could delete important data' | Comment entered |
| 3 | Click Submit/Confirm | Modal closes; card updates; action blocked |
| 4 | Verify toolkit tool does NOT execute | No execution |
| 5 | Verify LLM response acknowledges the block | LLM responds about the block |

---

## Expected Final State

Block with Comment recorded; toolkit action prevented.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Block with Comment works; toolkit not executed.

**Fail:**
- Any step produces an error or unexpected result.
- Toolkit executes or comment not recorded.
