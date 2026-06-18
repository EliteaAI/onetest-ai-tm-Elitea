---
id: ELITEA-0206
title: "Multiple Users Maintain Independent Model Overrides on Same Published Agent"
priority: medium
type: functional
module: agents-studio
status: draft
execution_type: manual
tags: [feat: agent-publishing, meta:needs_refinement, r-2.0.3, 4644]
requirements: [EliteaAI/elitea_issues#4644]
---
# ELITEA-0206: Multiple Users Maintain Independent Model Overrides on Same Published Agent

**Module:** Agents Studio · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that two users accessing the same published agent simultaneously can each apply different model overrides that do not interfere with each other.

**Coverage:**
- Session isolation for model overrides across different users

## Preconditions

- Two browser sessions logged in as different users (User A, User B) with access to the same published agent

## Test Data

User A override: Anthropic Claude 4.6 Sonnet
User B override: GPT-5.4-mini

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | User A opens the published agent and switches model to Anthropic Claude 4.6 Sonnet. Sends a message. | Valid response; toolbar shows Anthropic Claude 4.6 Sonnet. |
| 2 | Simultaneously, User B opens the same published agent and switches model to GPT-5.4-mini. Sends a message. | Valid response; toolbar shows GPT-5.4-mini. |
| 3 | Verify User A's toolbar still shows Anthropic Claude 4.6 Sonnet (not affected by User B's selection). | Confirmed — overrides are independent. |

## Expected Final State

Confirmed — overrides are independent.

## Pass/Fail Criteria

**Pass:**
- Each user's override is isolated to their own session
- No cross-user model leakage

**Fail:**
- User B's selection overrides User A's model or vice versa
