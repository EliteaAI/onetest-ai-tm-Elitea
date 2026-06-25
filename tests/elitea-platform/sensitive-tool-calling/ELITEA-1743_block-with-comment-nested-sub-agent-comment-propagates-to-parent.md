---
id: ELITEA-1743
title: "Block with Comment in Nested Sub-Agent — Comment Propagates to Parent as user_feedback"
priority: high
type: functional
module: sensitive-tool-calling
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5318]
---
# ELITEA-1743: Block with Comment in Nested Sub-Agent — Comment Propagates to Parent

**Module:** Sensitive Tool Calling · **Priority:** High · **Type:** Functional

**Objective:** Verify that when a sub-agent's sensitive tool is blocked with a comment, the `user_feedback` comment is propagated through the sub-agent's blocked ToolMessage result back to the parent agent's context, so the parent's response reflects the user's reason.

## Preconditions

- Parent agent has an Application sub-agent tool
- Sub-agent calls at least one sensitive tool
- Authorization dialog appears attributed to the sub-agent's sensitive tool

## Test Data

| Field | Value |
|-------|-------|
| Parent agent | Agent with sub-agent Application tool |
| Sub-agent | Agent that calls at least one tool marked as sensitive |
| Comment | "Do not proceed — use an alternative approach instead" |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Send a prompt to the parent agent that causes it to delegate to the sub-agent | Parent dispatches sub-agent |
| 2 | Sub-agent runs and hits the sensitive tool | HITL authorization dialog appears (attributed to the sub-agent's tool) |
| 3 | Click Block with Comment, enter the test comment, submit | Dialog closes |
| 4 | Observe the sub-agent's blocked result | Sub-agent receives a blocked ToolMessage containing the `user_feedback` comment |
| 5 | Observe the parent agent's final response | Parent's response references the user's comment reason |
| 6 | Verify the sensitive tool did NOT execute | No side effect from the sensitive tool |

## Expected Final State

Comment propagated from HITL dialog → sub-agent blocked ToolMessage → parent context. Parent response reflects user's stated reason.

## Pass/Fail Criteria

**Pass:**
- Sub-agent's blocked result includes `user_feedback` with the comment
- Parent agent response reflects the comment reason
- Sensitive tool did NOT execute
- No crash or context corruption at the parent level

**Fail:**
- Comment not passed to sub-agent's ToolMessage result
- Parent produces generic "sub-agent blocked" message without comment
- Sub-agent or parent crashes after block
- Tool executes despite block
