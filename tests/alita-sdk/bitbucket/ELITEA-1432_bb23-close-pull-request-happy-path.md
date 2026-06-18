---
id: ELITEA-1432
title: "BB23 - Close Pull Request - Happy Path"
priority: high
type: functional
module: bitbucket
status: ready
execution_type: automated
tags: [close_pull_request, pull-request, bitbucket, smoke]
requirements: []
---
# ELITEA-1432: BB23 - Close Pull Request - Happy Path

**Module:** Bitbucket · **Priority:** High · **Type:** Functional

**Objective:** Verify the Bitbucket 'close_pull_request' tool closes a PR without merging (Cloud only). Full flow: creates source branch, adds test file, creates PR, closes it without merging, verifies PR status reflects closure, and cleans up branch.

## Preconditions

Bitbucket toolkit is configured and authenticated
BB_REPO and BB_WORKSPACE env vars are set
Repository is accessible with write permissions
BB_BASE_BRANCH exists as target for PR

## Test Data

BB_TOOLKIT_ID: Bitbucket toolkit ID
BB_TOOLKIT_NAME: Bitbucket toolkit name
BB_REPO: Target repository name
BB_WORKSPACE: Bitbucket workspace slug
BB_BASE_BRANCH: Target/destination branch for PR
Source branch: 'test-close-pr-{timestamp}'
Expected PR status after close: DECLINED or CLOSED (not OPEN or MERGED)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call create_branch to create test source branch (e.g., 'test-close-pr-{timestamp}') | Source branch created successfully |
| 2 | Call set_active_branch to switch to the source branch | Active branch switched to source branch |
| 3 | Call create_file on source branch to add a test file creating a commit ahead of target | Test file created on source branch |
| 4 | Build PR JSON payload and call create_pull_request to create PR from source to BB_BASE_BRANCH | PR created successfully, response contains PR ID |
| 5 | Extract the new PR ID from the create_pull_request response | PR ID extracted from response |
| 6 | Call close_pull_request with the extracted PR ID (without merging) | PR closed successfully without merging, success response returned |
| 7 | Call get_pull_request with the PR ID to verify PR status reflects closure (DECLINED/CLOSED state) | PR status shows DECLINED or CLOSED, not OPEN |
| 8 | LLM validates: PR was created, then closed without merging, status confirms closure, full lifecycle completed | Validation confirms close_pull_request correctly closes PR without merging |
| 9 | Cleanup: call delete_branch to remove the test source branch | Source branch deleted, repository cleaned up |

## Expected Final State

Source branch deleted, repository cleaned up

## Pass/Fail Criteria

PASS: Full PR lifecycle completes — branch created, file added, PR created, PR closed, status verified as closed, branch cleaned up
FAIL: Any step in the lifecycle fails, PR status not showing closed after close operation
