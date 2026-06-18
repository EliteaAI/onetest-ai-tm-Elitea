---
id: ELITEA-0207
title: "Model Settings Override Persists Across In-Session Page Navigation"
priority: medium
type: functional
module: agents-studio
status: draft
execution_type: manual
tags: [feat: agent-publishing, meta:needs_refinement, r-2.0.3, 4644]
requirements: [EliteaAI/elitea_issues#4644]
---
# ELITEA-0207: Model Settings Override Persists Across In-Session Page Navigation

**Module:** Agents Studio · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that a model override applied in a published agent chat session is retained if the user navigates away and returns to the same conversation within the same browser session.

**Coverage:**
- Override not lost on in-session navigation

## Preconditions

- Published agent is open in chat, model override has been applied

## Test Data

Override model: GPT-5.4

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open published agent in chat, switch model to GPT-5.4. | Toolbar shows GPT-5.4. |
| 2 | Navigate to another page (e.g. Agents list). | Page changes. |
| 3 | Navigate back to the same conversation. | Conversation is still displayed. |
| 4 | Observe the model selector in the toolbar. | GPT-5.4 is still shown (override preserved). |

## Expected Final State

GPT-5.4 is still shown (override preserved).

## Pass/Fail Criteria

**Pass:**
- Model override GPT-5.4 is retained after returning to the conversation

**Fail:**
- Model resets to agent default after in-session navigation
