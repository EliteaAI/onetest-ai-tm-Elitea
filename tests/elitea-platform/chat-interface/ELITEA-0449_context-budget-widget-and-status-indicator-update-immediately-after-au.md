---
id: ELITEA-0449
title: "Context Budget Widget and Status Indicator Update Immediately After Auto-Summarization"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:chat, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3840]
---
# ELITEA-0449: Context Budget Widget and Status Indicator Update Immediately After Auto-Summarization

**Module:** Chat Interface · **Priority:** High · **Type:** Functional

**Objective:** Verify that the Context Budget widget reflects reduced token usage and the collapsed-view status indicator transitions from orange to green immediately after automatic summarization completes — without requiring the user to send an additional message.

**Coverage:**
- Context Budget widget transitions out of overloaded state in the same message turn that triggered summarization
- Collapsed-view status line changes from orange (>100%) to green (≤100%) immediately after summarization
- No extra user message needed for either the widget state or the status indicator to update
- Orange overloaded state is not retained after summarization is complete

## Preconditions

- Logged in to {{base_url}} as a user with access to a private project
- Chrome browser (latest stable)

## Test Data

- Max Context Tokens: `1000`
- Target Summary Tokens: `200`
- Min Messages for Summary: `3`
- Context-overflow trigger message: `Give me an extensive biography of Naruto`
- Summarization trigger message: `Hello`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chat in the left sidebar; click Create to open a new conversation. | New conversation is displayed with the chat input visible. |
| 2 | Send any short message (e.g., `Hi`) to initialize the conversation and reveal the Context Budget widget in the right PARTICIPANTS panel. | Context Budget widget appears in the PARTICIPANTS panel. |
| 3 | Click Edit context settings on the Context Budget widget → set Max Context Tokens to `1000`, Target Summary Tokens to `200`, Min Messages for Summary to `3`; ensure Context Management toggle is ON and Enable Automatic Summarization toggle is ON. Save settings. Keep the widget in Collapsed view. | Settings are saved. Collapsed status line is visible. |
| 4 | Send the token-overflow message: `Give me an extensive biography of Naruto`. | AI responds. Context Budget widget enters overloaded state — collapsed status line is orange (>100%). |
| 5 | Send a short follow-up message: `Hello` to trigger automatic summarization. | AI processes the message. Summarization activity is visible in the chat response. |
| 6 | Immediately after summarization completes and before sending any additional message, observe the Context Budget widget and the collapsed status line indicator. | (a) Status line has changed from orange to green (≤100%). (b) Widget no longer reflects the overloaded state — token usage is reduced. |

## Expected Final State

(a) Status line has changed from orange to green (≤100%). (b) Widget no longer reflects the overloaded state — token usage is reduced.

## Pass/Fail Criteria

**Pass:**
- After step 6, the collapsed status indicator is green and the widget reflects reduced/normal token usage — without sending another message
- Both the widget state and the status indicator update within the same response turn that triggered summarization

**Fail:**
- Widget or collapsed status indicator remains orange/overloaded after summarization completes
- Either the widget or the indicator only updates after the user sends one more additional message
