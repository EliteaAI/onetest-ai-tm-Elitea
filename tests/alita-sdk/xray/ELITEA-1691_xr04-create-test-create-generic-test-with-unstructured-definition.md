---
id: ELITEA-1691
title: "XR04 - create_test: Create Generic Test with Unstructured Definition"
priority: high
type: functional
module: xray
status: failed
execution_type: automated
tags: []
requirements: []
---
# ELITEA-1691: XR04 - create_test: Create Generic Test with Unstructured Definition

**Module:** Xray · **Priority:** High · **Type:** Functional

**Objective:** Verify the Xray create_test tool successfully creates a Generic test type with unstructured content.

Preconditions:
- Xray Cloud integration is configured
- User has permission to create tests in the target project

## Preconditions

Xray Cloud integration is configured with valid API credentials.
User has permission to create tests in the target project.
Project key EL (or XRAY_PROJECT_KEY) is accessible.

## Test Data

project_key: EL (configurable via XRAY_PROJECT_KEY)
test_summary: auto-generated — format: "XR04 Generic Test {timestamp}-{random_suffix}"
unstructured content: exploratory testing instructions for a calculator app (5 focus areas: arithmetic ops, edge cases, UI responsiveness, error handling, keyboard shortcuts)
labels: ["ELITEA_AI_CREATED"]

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure Xray Cloud toolkit using XRAY_TOOLKIT_ID and XRAY_TOOLKIT_NAME | Toolkit initialized successfully |
| 2 | Generate a unique test summary: 'XR04 Generic Test {timestamp}-{random_suffix}' | Unique test summary is generated |
| 3 | Build a GraphQL mutation to create a Generic test with unstructured exploratory testing content (multiline instructions for calculator testing), project key, description, and label ELITEA_AI_CREATED — requesting fields: issueId, testType (name, kind), unstructured, jira key/summary/labels | GraphQL mutation is prepared correctly for Generic test type |
| 4 | Call `create_test` tool with the prepared GraphQL mutation | Tool executes without throwing an exception |
| 5 | Extract test key (format: PROJECT-###) from the creation result using regex | Test key is extracted |
| 6 | LLM validator verifies: test_created=true, has_issue_id=true, has_test_key=true, correct_type='Generic', has_unstructured=true, no_errors=true | test_results: {test_passed: true, tool_executed: true, no_errors: true, test_created: true, has_issue_id: true, has_test_key: true, correct_type: true, has_unstructured: true} |

## Expected Final State

test_results: {test_passed: true, tool_executed: true, no_errors: true, test_created: true, has_issue_id: true, has_test_key: true, correct_type: true, has_unstructured: true}

## Pass/Fail Criteria

test_passed = true
tool_executed = true
no_errors = true
test_created = true
has_issue_id = true
has_test_key = true
correct_type = true (Generic)
has_unstructured = true
