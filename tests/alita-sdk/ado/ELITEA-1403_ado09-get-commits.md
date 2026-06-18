---
id: ELITEA-1403
title: "ADO09 - Get Commits"
priority: medium
type: functional
module: ado
status: ready
execution_type: automated
tags: [repository, toolkit, sdk, ado]
requirements: []
---
# ELITEA-1403: ADO09 - Get Commits

**Module:** Ado · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the ADO 'get_commits' tool returns commits for a path or branch

## Preconditions

ADO Repos toolkit is configured with valid credentials.
ADO_REPOSITORY_ID is set.
Repository has commits on the main branch.

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure ADO Repos toolkit with the target repository ID | Toolkit initialized successfully |
| 2 | Call `get_commits` tool with repository_id and optionally a branch or path parameter | Tool executes without error |
| 3 | Verify at least 1 commit is returned in the response | Response contains a list with at least 1 commit entry |
| 4 | Verify each commit entry has basic metadata (commit ID, author, or date) | Commit entries contain identifiable metadata fields |
| 5 | Validate no error message is present in the result | Result does not contain 'error' or 'failed' |

## Expected Final State

Result does not contain 'error' or 'failed'

## Pass/Fail Criteria

test_passed = true
tool_executed = true
commit_count >= 1
no_error = true
