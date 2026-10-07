---
id: ELITEA-3706
title: "Verify Cost and Tokens Split Correctly When Switching Models Mid-Conversation"
priority: high
type: functional
module: analytics
status: draft
execution_type: manual
tags: [feat:analytics, r-2.0.7, bug-env:dev, bug-area:current-release-scope]
requirements: [EliteaAI/elitea_issues#6574]
---

# ELITEA-3706: Verify Cost and Tokens Split Correctly When Switching Models Mid-Conversation

**Module:** Analytics · **Priority:** High · **Type:** Functional

**Objective:** Verify cost and tokens are attributed to the correct model when the participant model is changed partway through a conversation.

**Coverage:**
- Each message's cost/tokens attributed to the model that actually served it, not merged under one model

## Preconditions

- Access to Analytics "by Model" breakdown
- Two distinct platform-managed models available in one conversation

## Test Data

| Field | Value |
|-------|-------|
| Model A / Model B | Two distinct platform-managed chat models |
| Message 1 / Message 2 | "Hello from Model A" / "Hello from Model B" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Start a chat on Model A and send Message 1 | Model A responds |
| 2 | Switch the conversation's model participant to Model B | Switch succeeds, same conversation |
| 3 | Send Message 2 in the same conversation | Model B responds |
| 4 | Open Analytics > Costs/Tokens "by Model" breakdown for this window | Model A shows cost/tokens for Message 1 only; Model B shows cost/tokens for Message 2 only |

## Expected Final State

Each message's cost/tokens are attributed to the model that actually served it, not merged under a single model.

## Pass/Fail Criteria

**Pass:**
- Model A's and Model B's rows each reflect only their own message

**Fail:**
- Both messages' cost/tokens are attributed to a single model
