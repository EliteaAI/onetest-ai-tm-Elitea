---
id: ELITEA-3797
title: "Block with Comment — Tool Does NOT Execute and Comment Is Sent to LLM"
priority: critical
type: functional
module: sensitive-tool-calling
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5318]
---
# ELITEA-3797: Block with Comment — Tool Does NOT Execute and Comment Is Sent to LLM

**Module:** Sensitive Tool Calling · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that clicking "Block with Comment" after entering a reason prevents the sensitive tool from executing and passes the user's comment to the LLM so the agent's response reflects it.

## Preconditions

- At least one tool marked as sensitive in guardrails configuration
- Authorization dialog is currently displayed in the agent chat
- Comment input field is visible (Block with Comment was already clicked)

## Test Data

| Field | Value |
|-------|-------|
| Tool | Any tool marked as sensitive in guardrails configuration |
| Comment | "Do not proceed with this action — use an alternative approach instead" |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Ensure the Block with Comment text input is visible | Text area is displayed and focused |
| 2 | Type the test comment into the text area | Comment text appears in the input field |
| 3 | Submit with ⌘/Ctrl+Enter or click the **Block with Comment** confirm button | Dialog closes immediately |
| 4 | Observe agent's response in chat | Agent produces a text response acknowledging the block |
| 5 | Verify the agent's response references the user's comment | Agent response mentions "alternative approach" or the stated reason — not a generic blocked message |
| 6 | Verify the sensitive tool did NOT execute | No side effect from the sensitive tool |
| 7 | Verify chat input and Send button are re-enabled | Input field and Send button are active |

## Expected Final State

Tool blocked. Agent response incorporates the user's comment and the stated reason. No side effect from the sensitive tool.

## Pass/Fail Criteria

**Pass:**
- Dialog closes on submit
- Tool does NOT execute (no side effect)
- Agent response reflects the user's comment reason
- Chat input re-enabled after response

**Fail:**
- Tool executes despite Block with Comment
- Agent produces generic "blocked" message without incorporating comment
- Chat remains stuck after submit
- Comment text lost or not passed to agent
