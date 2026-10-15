---
id: ELITEA-0856
title: "Pipeline Execution - Message Flow and History"
priority: high
type: functional
module: pipelines
status: ready
execution_type: automated
automation_test_id:
  - tests.ui.pipelines.test_pipeline_execution.TestExecutePipeline.test_message_count_starts_at_zero_and_grows
  - tests.ui.pipelines.test_pipeline_execution.TestExecutePipeline.test_message_count_after_execution
  - tests.ui.pipelines.test_pipeline_execution.TestExecutePipeline.test_rerun_pipeline
  - tests.ui.pipelines.test_pipeline_execution.TestPipelineChatMessages.test_user_message_visible
  - tests.ui.pipelines.test_pipeline_execution.TestPipelineChatMessages.test_multiple_executions_accumulate
  - tests.ui.pipelines.test_pipeline_execution.TestPipelineExecutionEdgeCases.test_navigate_away_and_reexecute
tags: []
requirements: []
---
# ELITEA-0856: Pipeline Execution - Message Flow and History

**Module:** Pipelines · **Priority:** High · **Type:** Functional

**Objective:** Verify pipeline execution behavior: message count tracking, chat history accumulation, user messages visibility, and rerun functionality.

**Coverage:**
- Message count increments after execution
- Rerun pipeline produces new response
- User message visible in chat after execution
- Multiple executions accumulate in chat history
- Navigate away and return, then re-execute pipeline

## Preconditions

- User is logged in to {{base_url}} via Keycloak
- A pipeline with at least one LLM node exists (create one manually: add LLM node, connect to END, save)
- AI model (gpt-5-mini) is available for pipeline execution
- Browser: Chrome or Chromium

## Test Data

- URL: {{base_url}}
- Test messages: Hello, Say hello, First message, Second message, What is 2+2?, Color of sky?, Name a fruit
- Expected: each message produces a user + AI response pair
- Timeout: allow up to 90 seconds for pipeline execution

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open a pipeline that has at least one LLM node connected to END. Look at the embedded chat panel on the right side. Verify it shows no messages. | The embedded chat panel is empty with 0 messages. |
| 2 | Type 'Hello' in the message input field of the embedded chat and send it. Wait for the AI response (up to 90 seconds). | The message count increases to at least 2 (your message + AI response). The response contains non-empty text. |
| 3 | Send a second message (e.g., 'Second message') and wait for the response. | The message count increases by at least 2 more from the previous count. |
| 4 | Scroll through the chat history and verify your original 'Hello' message is visible in the list. | The user message text is visible in the chat message list. |
| 5 | Send 3 more messages one by one ('What is 2+2?', 'Color of sky?', 'Name a fruit'), waiting for each response. | All messages get responses. Total message count is at least 6 (3 user + 3 AI). The last response is non-empty. |
| 6 | Navigate away to the Pipelines list page, then return to the same pipeline. Send another message. | The pipeline re-executes successfully. The response does not contain 'unexpected error'. |

## Expected Final State

The pipeline re-executes successfully. The response does not contain 'unexpected error'.

## Pass/Fail Criteria

**Pass:**
- Initial message count is 0
- Each execution adds >= 2 messages (user + AI)
- Rerun produces new responses
- User messages visible in chat history
- Multiple executions accumulate correctly
- Re-execution works after navigation away and back

**Fail:**
- Pipeline execution times out (> 90s)
- Message count doesn't increment
- User message text not found in history
- Response contains "unexpected error"
- Re-execution fails after navigation
