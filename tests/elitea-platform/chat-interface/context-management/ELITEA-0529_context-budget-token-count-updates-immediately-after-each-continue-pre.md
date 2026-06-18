---
id: ELITEA-0529
title: "Context Budget Token Count Updates Immediately After Each Continue Press [Parametrized]"
priority: critical
type: functional
module: context-management
status: ready
execution_type: manual
tags: [feat:context-management, r-2.0.2]
requirements: [EliteaAI/elitea_issues#4474]
---
# ELITEA-0529: Context Budget Token Count Updates Immediately After Each Continue Press [Parametrized]

**Module:** Context Management · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the Context Budget token count updates immediately after each Continue press — without requiring a new user message.

**Coverage:**
- Token count is not stale after clicking Continue
- Token count increments on each subsequent Continue press
- Verified on Chat, Agent, and Pipeline pages

## Preconditions

- Logged in to {{base_url}}
- Context Budget widget visible after first message

## Test Data

| Parameter | Value |
|---|---|
| Pages (run once each) | Chat conversation, Agent conversation, Pipeline conversation |
| LLM model | Any non-reasoning model (for easier reproduction) (e.g., GPT-4o) |
| Max Completion Tokens | Custom → 3 |
| Test message | "hi" |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open a new conversation on the target page (Chat / Agent / Pipeline). Open model settings, select a non-reasoning LLM (e.g., GPT-4o), and set Max Completion Tokens → Custom → 3. | Conversation is open with the token limit set to 3. |
| 2 | Note the current token count in the Context Budget widget. | Baseline token count is recorded. |
| 3 | Send the message: "hi". | "Token limit reached mid-response. Press 'Continue' to see more." prompt appears. |
| 4 | Note the token count shown at the pause point, then click Continue. Wait for the response to finish. | Response completes. Context Budget widget token count increases compared to the pause-point value — without sending another message. |
| 5 | If the token limit is hit again, click Continue a second and third time, noting the token count after each. | Token count increases after each Continue press. No stale/unchanged value observed between presses. |
| 6 | Repeat Steps 1–5 for each remaining page type (Chat, Agent, Pipeline). | Token count updates immediately after Continue on all three page types. |

## Expected Final State

Token count updates immediately after Continue on all three page types.

## Pass/Fail Criteria

**Pass:**
- Token count updates in the Context Budget widget immediately after each Continue press and response completion
- No stale token count observed between Continue presses
- Consistent behavior across Chat, Agent, and Pipeline pages

**Fail:**
- Token count stays unchanged after Continue and response completion
- Token count only updates after the next user message is sent
- Widget shows stale state on any of the three page types
