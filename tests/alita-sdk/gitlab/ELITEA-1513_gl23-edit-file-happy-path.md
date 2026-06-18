---
id: ELITEA-1513
title: "GL23 - Edit File (Happy Path)"
priority: high
type: functional
module: gitlab
status: ready
execution_type: automated
tags: [edit_file, gitlab, files]
requirements: []
---
# ELITEA-1513: GL23 - Edit File (Happy Path)

**Module:** Gitlab · **Priority:** High · **Type:** Functional

**Objective:** Test edit_file applies targeted edits to an existing file (line-level or block-level changes): create branch, create file with initial content, edit file using edit_file tool, verify changes are applied, clean up.

## Preconditions

GitLab toolkit is configured and authenticated
GITLAB_TOOLKIT_NAME env var is set
Write access to repository

## Test Data

GITLAB_TOOLKIT_NAME: configured GitLab toolkit name
Branch name: test/gl23-edit-file-<timestamp>
File path: test/gl23_edit.txt
Initial content: "Line 1: keep this
Line 2: change this
Line 3: keep this"
Edit: replace "change this" with "changed by GL23 edit_file"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure GitLab toolkit and set GITLAB_TOOLKIT_NAME | Toolkit authenticated |
| 2 | Invoke create_branch to create a test branch | Test branch created |
| 3 | Invoke create_file with multi-line initial content on the branch | File created with initial content |
| 4 | Invoke edit_file specifying the file path, the old text to replace, and the new text | Targeted edit applied to the file |
| 5 | Invoke read_file to verify the edit was applied correctly | File contains the new text where the old text was replaced |
| 6 | Confirm the rest of the file content is unchanged | Only the targeted section was modified |
| 7 | Invoke delete_branch to clean up | Test branch deleted |

## Expected Final State

Test branch deleted

## Pass/Fail Criteria

create_branch and create_file succeed
edit_file completes without error
File content after edit matches expected result
delete_branch succeeds
