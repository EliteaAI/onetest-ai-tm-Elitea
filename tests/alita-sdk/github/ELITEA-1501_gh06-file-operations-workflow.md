---
id: ELITEA-1501
title: "GH06 - File Operations Workflow"
priority: critical
type: functional
module: github
status: ready
execution_type: automated
tags: [apply_git_patch, delete_file, create_file, workflow, github, files]
requirements: []
---
# ELITEA-1501: GH06 - File Operations Workflow

**Module:** Github · **Priority:** Critical · **Type:** Functional

**Objective:** Test full file lifecycle: create branch, set active branch, create file, read file to verify content, apply git patch to modify it, read file again to verify patch, then delete file and clean up.

## Preconditions

GitHub toolkit is configured and authenticated
GITHUB_TOOLKIT_NAME env var is set
Write access to the target repository (branch creation and file operations enabled)
Token has repo scope

## Test Data

GITHUB_TOOLKIT_NAME: configured GitHub toolkit name
GITHUB_REPO: target repository with write access
Branch name: test/gh06-file-ops-\u003ctimestamp\u003e
File path: test/gh06_sample.txt
Initial content: "Hello from GH06 test"
Patch: unified diff adding a second line to the file

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure GitHub toolkit with write access and set GITHUB_TOOLKIT_NAME | Toolkit authenticated with write permissions |
| 2 | Invoke create_branch with a unique branch name (e.g., test/gh06-<timestamp>) | Branch created successfully |
| 3 | Invoke set_active_branch to switch to the new branch | Active branch set to newly created branch |
| 4 | Invoke create_file to add a test file with known content on the branch | File created on branch with expected content |
| 5 | Invoke read_file to verify file content matches what was created | File content matches original creation input |
| 6 | Invoke apply_git_patch with a valid unified diff patch modifying the created file | Patch applied successfully, file modified |
| 7 | Invoke read_file again to verify the patch was applied correctly | File content reflects the patches changes |
| 8 | Invoke delete_file to remove the test file from the branch | File deleted from branch without error |
| 9 | Confirm cleanup and no residual test artifacts on the branch | Branch is clean after test file deletion |

## Expected Final State

Branch is clean after test file deletion

## Pass/Fail Criteria

create_branch returns valid branch name
set_active_branch switches to new branch
create_file creates file with expected content
First read_file returns original content
apply_git_patch modifies file as defined in patch
Second read_file returns patched content
delete_file removes file without error
All tools complete without error throughout workflow
