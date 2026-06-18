---
id: ELITEA-1520
title: "GL11 - Update File (Happy Path)"
priority: high
type: functional
module: gitlab
status: ready
execution_type: automated
tags: [update_file, gitlab, files]
requirements: []
---
# ELITEA-1520: GL11 - Update File (Happy Path)

**Module:** Gitlab · **Priority:** High · **Type:** Functional

**Objective:** Test update_file replaces existing file content: create branch, create file with initial content, update file with new content, verify new content is present, clean up.

## Preconditions

GitLab toolkit is configured and authenticated
GITLAB_TOOLKIT_NAME env var is set
Write access to repository

## Test Data

GITLAB_TOOLKIT_NAME: configured GitLab toolkit name
Branch name: test/gl11-update-file-<timestamp>
File path: test/gl11_update.txt
Initial content: "Original content line 1"
Updated content: "Updated content line 1 - modified by GL11"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure GitLab toolkit and set GITLAB_TOOLKIT_NAME | Toolkit authenticated |
| 2 | Invoke create_branch to create a test branch | Test branch created |
| 3 | Invoke create_file with initial content | File created with initial content |
| 4 | Invoke update_file with new/replacement content for the same file | File content replaced with new content |
| 5 | Invoke read_file to verify the file now contains updated content only | File content matches new content; original content replaced |
| 6 | Invoke delete_branch to clean up | Test branch deleted |

## Expected Final State

Test branch deleted

## Pass/Fail Criteria

create_branch and create_file succeed
update_file completes without error
File content after update matches the new content (not original)
delete_branch succeeds
