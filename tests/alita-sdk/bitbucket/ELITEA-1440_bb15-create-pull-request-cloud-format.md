---
id: ELITEA-1440
title: "BB15 - Create Pull Request - Cloud Format"
priority: high
type: functional
module: bitbucket
status: ready
execution_type: automated
tags: [create_pull_request, pull-request, bitbucket, smoke]
requirements: []
---
# ELITEA-1440: BB15 - Create Pull Request - Cloud Format

**Module:** Bitbucket · **Priority:** High · **Type:** Functional

**Objective:** Verify the Bitbucket 'create_pull_request' tool creates a PR using Cloud format. Tests source branch creation, adding test file to source branch, PR creation using cloud JSON format, and validates PR ID or URL is returned.

## Preconditions

Bitbucket toolkit is configured and authenticated
BB_REPO and BB_WORKSPACE env vars are set
Repository is accessible with write permissions
BB_BASE_BRANCH exists as target branch for PR

## Test Data

BB_TOOLKIT_ID: Bitbucket toolkit ID
BB_TOOLKIT_NAME: Bitbucket toolkit name
BB_REPO: Target repository name
BB_WORKSPACE: Bitbucket workspace slug
BB_BASE_BRANCH: Target/destination branch for PR
Source branch: 'test-pr-source-{timestamp}'
PR title: 'Test PR - BB15'
PR format: Bitbucket Cloud JSON

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call create_branch to create the PR source branch (e.g., 'test-pr-source-{timestamp}') | Source branch created successfully |
| 2 | Call set_active_branch to switch to the source branch | Active branch switched to source branch |
| 3 | Call create_file on source branch to add a test file (ensures branch has changes ahead of target) | Test file created on source branch |
| 4 | Build pull request JSON payload using Bitbucket Cloud format: {source: branch, destination: BB_BASE_BRANCH, title: 'Test PR', description: '...'} | PR JSON payload built correctly with Cloud format |
| 5 | Call create_pull_request with the cloud format PR JSON payload | PR created successfully, response contains PR ID or URL |
| 6 | LLM validates: PR was created successfully using cloud format, PR ID or URL is present in response | Validation confirms create_pull_request works with Bitbucket Cloud JSON structure |
| 7 | Cleanup: call delete_branch to remove the test source branch | Source branch deleted |

## Expected Final State

Source branch deleted

## Pass/Fail Criteria

PASS: PR created successfully, PR ID or URL returned in response, source branch and file exist
FAIL: PR creation fails, no PR ID returned, source branch or file missing
