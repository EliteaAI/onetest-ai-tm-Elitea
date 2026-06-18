---
id: ELITEA-1405
title: "ADO07 - Comment on Pull Request (simple)"
priority: medium
type: functional
module: ado
status: ready
execution_type: automated
tags: [pull-requests, toolkit, sdk, ado]
requirements: []
---
# ELITEA-1405: ADO07 - Comment on Pull Request (simple)

**Module:** Ado · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the ADO 'comment_on_pull_request' tool can add a general comment using comment_query format

## Preconditions

ADO Repos toolkit is configured with valid credentials.
PR #10 'PR FOR AI TEST' exists and is open.

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure ADO Repos toolkit with valid credentials | Toolkit initialized successfully |
| 2 | Call `comment_on_pull_request` tool with pull_request_id = '10' and a comment text using comment_query format | Tool executes without error |
| 3 | Verify the response indicates the comment was added successfully | Response contains success confirmation (e.g., comment ID or 'created') |
| 4 | Validate no error message is present in the result | Result does not contain 'error' or 'failed' |

## Expected Final State

Result does not contain 'error' or 'failed'

## Pass/Fail Criteria

test_passed = true
tool_executed = true
comment_added = true
no_error = true
