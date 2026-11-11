---
id: ELITEA-4685
title: "Target Summary Tokens Inheritance Into New Chat Agent and Pipeline Conversations Still Works"
priority: high
type: regression
module: context-management
status: draft
execution_type: manual
regression: true
tags: [feat:context-management, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6898]
---

## Preconditions

- User is logged in to `{{base_url}}`
- Existing manual coverage: ELITEA-0422, ELITEA-0423

## Test Data

| Field | Value |
|-------|-------|
| Target Summary Tokens | 200 (custom value distinct from default 4096) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Set Target Summary Tokens to 200 in Settings → Memory and save. | Value saves successfully. |
| 2 | Create a new Chat conversation, send a message, and open its Context Management modal. | The Summarization section (now positioned below the new Context window section) shows Target Summary Tokens = 200. |
| 3 | Create a new Agent chat session, send a message, and open its Context Management modal. | Target Summary Tokens = 200 is inherited here as well. |
| 4 | Create/access a new Pipeline chat session, trigger a run or message, and open its Context Management modal. | Target Summary Tokens = 200 is inherited here as well. |

## Expected Final State

The custom Target Summary Tokens value propagates correctly into new Chat, Agent, and Pipeline conversations, unaffected by the new Context window section added above Summarization in the modal.

## Pass/Fail Criteria

**Pass:**
- All three conversation types (Chat, Agent, Pipeline) show the custom Target Summary Tokens value of 200
- The new Context window section does not interfere with the Summarization section's values

**Fail:**
- Any conversation type shows the default (4096) instead of the custom value
- The Context Management modal fails to open or display the Summarization section correctly
