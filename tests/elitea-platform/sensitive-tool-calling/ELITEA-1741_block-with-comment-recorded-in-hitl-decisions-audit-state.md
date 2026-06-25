---
id: ELITEA-1741
title: "Block with Comment — Action and Comment Recorded in hitl_decisions Audit State"
priority: high
type: functional
module: sensitive-tool-calling
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5318]
---
# ELITEA-1741: Block with Comment — Action and Comment Recorded in hitl_decisions Audit State

**Module:** Sensitive Tool Calling · **Priority:** High · **Type:** Functional

**Objective:** Verify that after a Block with Comment action, the `hitl_decisions` checkpoint state records `hitl_action: "block_with_comment"` and the `user_feedback` comment text — so the decision is auditable.

## Preconditions

- At least one tool marked as sensitive in guardrails configuration
- Developer access to agent checkpoint state (e.g., via backend logs, LangGraph state inspector, or API)
- Authorization dialog currently displayed

## Test Data

| Field | Value |
|-------|-------|
| Tool | Any tool marked as sensitive in guardrails configuration |
| Comment | "Do not proceed — use an alternative approach instead" |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Trigger the sensitive tool dialog | Dialog displayed |
| 2 | Click Block with Comment, enter the test comment, and submit | Dialog closes; agent responds acknowledging the block |
| 3 | Inspect the LangGraph checkpoint state (or backend logs) for the agent thread | `hitl_decisions` entry exists for this tool call |
| 4 | Verify the `hitl_action` field | Value is `"block_with_comment"` (not `"block"` or `"reject"`) |
| 5 | Verify the `user_feedback` field | Value matches the comment entered: `"Do not proceed — use an alternative approach instead"` |
| 6 | Verify the tool call ID is correctly referenced | The decision is keyed to the correct tool call, not a stale or mismatched one |

## Expected Final State

Checkpoint state shows `hitl_action: "block_with_comment"` and `user_feedback` with the correct comment for the blocked tool call.

## Pass/Fail Criteria

**Pass:**
- `hitl_decisions` entry present with `hitl_action: "block_with_comment"`
- `user_feedback` matches entered comment
- Tool call ID correctly referenced

**Fail:**
- `hitl_action` stored as `"block"` or `"reject"` instead of `"block_with_comment"`
- `user_feedback` field absent or empty
- Decision keyed to wrong tool call
