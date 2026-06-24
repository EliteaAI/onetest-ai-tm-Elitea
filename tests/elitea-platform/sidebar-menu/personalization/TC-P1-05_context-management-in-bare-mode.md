---
id: TC-P1-05
title: "Verify Context Management Functions in Bare Mode"
priority: high
type: functional
module: sidebar-menu/personalization
status: ready
execution_type: manual
tags: [p1, bare-personality, context-management, summarization, r-2.0.4, 5264]
requirements: [EliteaAI/elitea_issues#5264]
---
# TC-P1-05: Verify Context Management Functions in Bare Mode

**Module:** Personalization · **Priority:** High · **Type:** Functional

**Objective:** Verify that context management features (automatic summarization, token tracking, message preservation) function correctly when "Bare" personality mode is active.

**Coverage:**
- Token usage displays correctly in Context Management modal
- Automatic summarization triggers when approaching token limit
- Summary is generated without errors
- Recent messages are preserved as configured
- Conversation continues normally after summarization

## Preconditions

- User has "Bare" personality selected
- Context management is enabled in User Settings
- Max Context Tokens is set to a low value (e.g., 1000) to trigger summarization quickly
- Preserve Recent Messages is set to 2
- Automatic summarization is enabled

## Test Data

- Personality: Bare
- Max Context Tokens: 1000
- Preserve Recent Messages: 2
- Test messages: Long-form questions about technical topics

## Steps

| # | Action | Expected Result |
|---|--------|----------------||
| 1 | Navigate to User Settings → Personalization. | Settings page opens. |
| 2 | Set Default Personality to "Bare". | "Bare" selected. |
| 3 | Open Context Management settings (click "Edit context settings" icon). | Context Management modal opens. |
| 4 | Configure: Max Context Tokens: 1000, Preserve Recent Messages: 2, Enable automatic summarization: ON. | Settings configured. |
| 5 | Set Summarization instructions: "Generate a concise summary of the following conversation messages." | Instructions entered. |
| 6 | Save context settings and start a new conversation. | New conversation created. |
| 7 | Send Message 1: "Explain quantum computing in detail" (wait for response). | Long response received. |
| 8 | Send Message 2: "Now explain machine learning algorithms" (wait for response). | Long response received. |
| 9 | Send Message 3: "Tell me about blockchain technology" (wait for response). | Long response received. |
| 10 | Open Context Management modal and check "Tokens" display (e.g., "950 / 1000 tokens"). | Token usage near limit. |
| 11 | Send Message 4 to trigger summarization: "What are ethical implications of AI?" | Message sent. |
| 12 | Wait for response and check Context Management modal. | Response received. |
| 13 | Verify "Summaries" count increases from 0 to 1. | Summary was created. |
| 14 | Verify token count drops after summarization (e.g., from 950 to 500). | Token count reduced. |
| 15 | Verify last 2 message pairs are preserved in chat interface. | Recent messages visible. |
| 16 | Check SDK logs for summarization process confirmation. | SDK logs show summarization completed. |
| 17 | Send another message to verify conversation continues normally. | Conversation works after summarization. |

## Expected Final State

Conversation history includes summary + recent messages. Token budget is managed correctly. No errors related to Bare mode affecting summarization.

## Pass/Fail Criteria

**Pass:**
- Context Management modal displays token usage correctly
- Automatic summarization triggers when approaching limit
- Summary is generated without errors
- Summaries count increases
- Recent messages (last 2) are preserved
- Older messages are summarized and compressed
- Token count drops after summarization
- Conversation continues normally
- No errors in SDK logs or console

**Fail:**
- Summarization fails to trigger
- Token counting is inaccurate
- Summary generation errors
- Recent messages are not preserved
- Token count doesn't drop after summarization
- Conversation breaks after summarization
- Errors related to missing system prompt or personality
