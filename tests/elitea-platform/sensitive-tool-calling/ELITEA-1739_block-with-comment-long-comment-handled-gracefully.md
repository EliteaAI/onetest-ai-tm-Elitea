---
id: ELITEA-1739
title: "Block with Comment — Long Comment Handled Gracefully"
priority: high
type: functional
module: sensitive-tool-calling
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5318]
---
# ELITEA-1739: Block with Comment — Long Comment Handled Gracefully

**Module:** Sensitive Tool Calling · **Priority:** High · **Type:** Functional

**Objective:** Verify that a very long comment submitted via Block with Comment does not break the dialog, crash the agent, or produce malformed LLM input — long comments are truncated or accepted without error.

## Preconditions

- Sensitive tool dialog is displayed
- Block with Comment text area is expanded

## Test Data

| Field | Value |
|-------|-------|
| Tool | Any tool marked as sensitive in guardrails configuration |
| Comment | 2000+ character string (e.g., "Do not proceed. " repeated 120 times) |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Paste 2000+ characters into the comment text area | Text is accepted (possibly truncated at a max length) |
| 2 | Submit the comment (⌘/Ctrl+Enter or confirm button) | Dialog closes without error |
| 3 | Observe the agent's response | Agent produces a coherent blocked-action response; no parsing error or crash |
| 4 | Verify the sensitive tool did NOT execute | No side effect from the sensitive tool |

## Expected Final State

Long comment handled without crash. Tool blocked. Agent response coherent.

## Pass/Fail Criteria

**Pass:**
- Long comment accepted (or gracefully truncated with UI feedback)
- No JS error / dialog crash
- Agent produces coherent response
- Tool does NOT execute

**Fail:**
- UI hangs or crashes on long input
- Agent receives malformed `user_feedback` and errors
- Backend returns 4xx/5xx error
- Dialog becomes unresponsive
