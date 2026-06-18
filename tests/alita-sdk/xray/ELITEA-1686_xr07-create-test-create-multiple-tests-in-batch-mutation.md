---
id: ELITEA-1686
title: "XR07 - create_test: Create Multiple Tests in Batch Mutation"
priority: medium
type: functional
module: xray
status: failed
execution_type: automated
tags: []
requirements: []
---
# ELITEA-1686: XR07 - create_test: Create Multiple Tests in Batch Mutation

**Module:** Xray · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the Xray create_test tool can create multiple tests in a single GraphQL mutation using aliases.

Preconditions:
- Xray Cloud integration is configured
- User has permission to create tests in the target project

## Preconditions

Xray Cloud integration is configured with valid API credentials.
User has permission to create tests in the target project.
Project key EL (or XRAY_PROJECT_KEY) is accessible.

## Test Data

project_key: EL (configurable via XRAY_PROJECT_KEY)
manual test summary: auto-generated — "XR07 Manual Batch Test {timestamp}-{suffix}"
generic test summary: auto-generated — "XR07 Generic Batch Test {timestamp}-{suffix}"
Manual test steps: 3-step login scenario (navigate to login → enter credentials → click login button)
Generic test content: security exploratory testing instructions (SQL injection, XSS, auth bypass, session management, error handling)
labels: ["ELITEA_AI_CREATED", "BATCH_TEST"]

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure Xray Cloud toolkit using XRAY_TOOLKIT_ID and XRAY_TOOLKIT_NAME | Toolkit initialized successfully |
| 2 | Generate unique summaries for both tests: 'XR07 Manual Batch Test {timestamp}-{suffix}' and 'XR07 Generic Batch Test {timestamp}-{suffix}' | Both unique summaries are generated |
| 3 | Build a single GraphQL mutation using aliases: 'manualTest: createTest(...)' for a 3-step login Manual test and 'genericTest: createTest(...)' for a security-focused Generic test — both labeled ELITEA_AI_CREATED and BATCH_TEST | Single combined mutation string is prepared with both aliased operations |
| 4 | Call `create_test` tool once with the combined aliased mutation (batch creation in a single API call) | Tool executes without throwing an exception |
| 5 | LLM validator checks that: both manualTest and genericTest aliases returned results, both have issueIds and Jira keys, no error indicators present | test_results: {test_passed: true, tool_executed: true, no_errors: true, has_manual_test: true, has_generic_test: true, has_issue_ids: true, has_keys: true, all_tests_created: true, tests_created_count: 2} |

## Expected Final State

test_results: {test_passed: true, tool_executed: true, no_errors: true, has_manual_test: true, has_generic_test: true, has_issue_ids: true, has_keys: true, all_tests_created: true, tests_created_count: 2}

## Pass/Fail Criteria

test_passed = true
tool_executed = true
no_errors = true
has_manual_test = true
has_generic_test = true
has_issue_ids = true
has_keys = true
all_tests_created = true
tests_created_count = 2
