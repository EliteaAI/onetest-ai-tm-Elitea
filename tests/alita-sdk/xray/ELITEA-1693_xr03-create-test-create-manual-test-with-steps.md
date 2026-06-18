---
id: ELITEA-1693
title: "XR03 - create_test: Create Manual Test with Steps"
priority: high
type: functional
module: xray
status: ready
execution_type: automated
tags: []
requirements: []
---
# ELITEA-1693: XR03 - create_test: Create Manual Test with Steps

**Module:** Xray · **Priority:** High · **Type:** Functional

**Objective:** Verify the Xray create_test tool successfully creates a Manual test type with multiple defined test steps.

Preconditions:
- Xray Cloud integration is configured
- User has permission to create tests in the target project
- AI TESTS folder exists in the project

## Preconditions

Xray Cloud integration is configured with valid API credentials.
User has permission to create tests in the target project.
AI TESTS folder exists in the project (folder ID: 698cb958abcc3edb91a6c42d).

## Test Data

project_key: EL (configurable via XRAY_PROJECT_KEY)
test_summary: auto-generated — format: "XR03 Manual Test {timestamp}-{random_suffix}"
Test steps: 5-step calculator scenario (open app → enter 5 → click + → enter 3 → click = → result is 8)
labels: ["ELITEA_AI_CREATED"]

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure Xray Cloud toolkit using XRAY_TOOLKIT_ID and XRAY_TOOLKIT_NAME | Toolkit initialized successfully |
| 2 | Generate a unique test summary using current timestamp and random suffix: 'XR03 Manual Test {timestamp}-{random_suffix}' | Unique test summary is generated |
| 3 | Build a GraphQL mutation to create a Manual test with 5 steps (calculator scenario), project key, description, and label ELITEA_AI_CREATED — requesting fields: issueId, testType, steps (id, action, data, result), jira key/summary/labels | GraphQL mutation string is prepared correctly |
| 4 | Call `create_test` tool with the prepared GraphQL mutation | Tool executes without throwing an exception |
| 5 | Extract test key (format: PROJECT-###) from the creation result using regex | Test key is extracted, e.g. EL-123 |
| 6 | LLM validator verifies: test_created=true, has_issue_id=true, has_test_key=true, correct_type='Manual', has_steps=true, no_errors=true | test_results: {test_passed: true, tool_executed: true, no_errors: true, test_created: true, has_issue_id: true, has_test_key: true, correct_type: true, has_steps: true} |

## Expected Final State

test_results: {test_passed: true, tool_executed: true, no_errors: true, test_created: true, has_issue_id: true, has_test_key: true, correct_type: true, has_steps: true}

## Pass/Fail Criteria

test_passed = true
tool_executed = true
no_errors = true
test_created = true
has_issue_id = true
has_test_key = true
correct_type = true (Manual)
has_steps = true
