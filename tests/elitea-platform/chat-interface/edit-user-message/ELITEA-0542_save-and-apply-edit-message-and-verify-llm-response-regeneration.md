---
id: ELITEA-0542
title: "Save and apply — edit message and verify LLM response regeneration"
priority: critical
type: functional
module: edit-user-message
status: draft
execution_type: manual
tags: [feat:chat, r-2.0.4]
requirements: [EliteaAI/elitea_issues#4942]
---
# ELITEA-0542: Save and apply — edit message and verify LLM response regeneration

**Module:** Edit User Message · **Priority:** Critical · **Type:** Functional

**Objective:** Verify the primary flow: editing the last message and clicking Save and apply triggers regeneration of the LLM response based on updated input.

**Coverage:**
- Updated message saved
- Regeneration triggered with loading state
- New response reflects edited content
- Previous response is replaced

## Preconditions

- User is logged in to ELITEA at {{base_url}}
- Browser: Chrome latest
- A Chat Conversation with a last user message and LLM response

## Test Data

- Original message: "What is the capital of France?"
- Edited message: "What is the capital of Japan?"
- Expected: new response should mention "Tokyo"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open a conversation where the last user message is "What is the capital of France?" (with a response mentioning "Paris"). Click the Edit icon. | Edit mode opens with "What is the capital of France?" pre-loaded. |
| 2 | Change the text to "What is the capital of Japan?" and click "Save and apply". | Edit mode closes. A loading/streaming indicator appears, indicating regeneration is in progress. |
| 3 | Wait for the new response to finish generating. Verify the last user message content. | The last user message now reads "What is the capital of Japan?" (updated content saved). |
| 4 | Verify the LLM response. | The new LLM response mentions "Tokyo" (reflects the edited question). The previous response about "Paris" is no longer visible. |

## Expected Final State

The new LLM response mentions "Tokyo" (reflects the edited question). The previous response about "Paris" is no longer visible.

## Pass/Fail Criteria

**Pass:**
- Message is updated to edited content
- Loading state is shown during regeneration
- New response reflects the edited prompt
- Previous response is replaced

**Fail:**
- Message is not updated
- No regeneration occurs
- Previous response remains alongside new one
- New response still answers original question
