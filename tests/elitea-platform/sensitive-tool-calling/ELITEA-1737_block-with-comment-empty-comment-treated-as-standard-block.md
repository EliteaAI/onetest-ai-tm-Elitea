---
id: ELITEA-1737
title: "Block with Comment — Empty Comment Treated as Standard Block"
priority: high
type: functional
module: sensitive-tool-calling
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5318]
---
# ELITEA-1737: Block with Comment — Empty Comment Treated as Standard Block

**Module:** Sensitive Tool Calling · **Priority:** High · **Type:** Functional

**Objective:** Verify that submitting Block with Comment with an empty text field is handled gracefully — the tool is still blocked and the agent is not given an empty `user_feedback` payload (treated equivalent to a standard Block).

## Preconditions

- At least one tool marked as sensitive in guardrails configuration
- Authorization dialog is displayed and Block with Comment text area is visible

## Test Data

| Field | Value |
|-------|-------|
| Tool | Any tool marked as sensitive in guardrails configuration |
| Comment | (empty — no text entered) |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Click **Block with Comment** to expand the text area | Text area is visible and empty |
| 2 | Leave the text area empty and attempt to submit (⌘/Ctrl+Enter or confirm button) | **Option A:** Submit is disabled / button greyed out until text is entered — OR — **Option B:** Submit proceeds and blocks the tool without passing a comment |
| 3 | Observe the dialog behavior | Dialog closes (or stays open with a validation hint if empty input is prevented) |
| 4 | Observe the agent's response | Agent produces a blocked-action acknowledgement; no `user_feedback` reference in the response |
| 5 | Verify the sensitive tool did NOT execute | No side effect from the sensitive tool |

## Expected Final State

Tool is blocked. Agent acknowledges the block without referencing any comment. No empty string injected into LLM context as `user_feedback`.

## Pass/Fail Criteria

**Pass:**
- Empty submit either disabled by UI or silently treated as standard block
- Tool does NOT execute
- Agent response does not reference a blank/empty comment
- No crash or unexpected error

**Fail:**
- Empty comment submitted and agent receives empty `user_feedback`, producing confusing output
- Tool executes
- UI crashes on empty submit
