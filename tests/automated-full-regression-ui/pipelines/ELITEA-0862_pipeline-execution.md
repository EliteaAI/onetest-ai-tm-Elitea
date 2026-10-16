---
id: ELITEA-0862
title: "Pipeline Execution"
priority: critical
type: functional
module: pipelines
status: ready
execution_type: automated
automation_test_id:
  - tests.ui.pipelines.test_pipeline_execution.TestExecutePipeline.test_pipeline_response_is_meaningful
  - tests.ui.pipelines.test_pipeline_execution.TestPipelineChatMessages.test_user_message_visible
tags: []
requirements: []
---
# ELITEA-0862: Pipeline Execution

**Module:** Pipelines · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that pipelines execute successfully, produce meaningful responses, can be re-run, and messages display in chat.

## Preconditions

- User logged into Elitea
- Pipeline with LLM node exists

## Test Data

- URL: {{base_url}}
- Test message: Hello, how are you?

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| ? | Open pipeline with LLM node | Pipeline editor loads |
| ? | Enter test message, click Send | Pipeline executes, progress indicator shows |
| ? | Wait for response | AI response appears in chat (~5s) |
| ? | Send another message | Pipeline re-runs, new response generated |

## Expected Final State

Pipeline re-runs, new response generated

## Pass/Fail Criteria

**Pass:**
- Pipeline executes without errors
- Response appears in chat
- Re-run produces new response
- Messages persist

**Fail:**
- Execution fails
- No response
- Re-run fails
- Messages disappear
