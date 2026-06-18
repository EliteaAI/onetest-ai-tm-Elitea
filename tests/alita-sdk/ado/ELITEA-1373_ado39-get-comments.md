---
id: ELITEA-1373
title: "ADO39 - Get Comments"
priority: medium
type: functional
module: ado
status: ready
execution_type: automated
tags: [work-items, toolkit, sdk, ado]
requirements: []
---
# ELITEA-1373: ADO39 - Get Comments

**Module:** Ado · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the ADO 'get_comments' tool retrieves comments from a work item

## Preconditions

ADO Work Items toolkit is configured with valid credentials.
A work item with known ID has at least one comment.

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure ADO Work Items toolkit with valid credentials | Toolkit initialized successfully |
| 2 | Call `get_comments` tool with a known work_item_id that has existing comments | Tool executes without error |
| 3 | Verify the response contains a list of comments | Response is a non-empty list of comment entries |
| 4 | Verify comment entries contain text and author metadata | Comment entries include 'text' or 'content' and author information |
| 5 | Validate no error message is present in the result | Result does not contain 'error' or 'failed' |

## Expected Final State

Result does not contain 'error' or 'failed'

## Pass/Fail Criteria

test_passed = true
tool_executed = true
comments_returned = true
no_error = true
