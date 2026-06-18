---
id: ELITEA-1444
title: "BB13 - Update File - Valid OLD/NEW Markers"
priority: high
type: functional
module: bitbucket
status: ready
execution_type: automated
tags: [update_file, bitbucket, smoke, files]
requirements: []
---
# ELITEA-1444: BB13 - Update File - Valid OLD/NEW Markers

**Module:** Bitbucket · **Priority:** High · **Type:** Functional

**Objective:** Verify the Bitbucket 'update_file' tool correctly updates file content using OLD/NEW marker syntax. Tests that file is created with initial content, update with OLD/NEW markers succeeds, only targeted section is modified, other content remains unchanged.

## Preconditions

Bitbucket toolkit is configured and authenticated
BB_REPO and BB_WORKSPACE env vars are set
Repository is accessible with write permissions

## Test Data

BB_TOOLKIT_ID: Bitbucket toolkit ID
BB_TOOLKIT_NAME: Bitbucket toolkit name
BB_REPO: Target repository name
BB_WORKSPACE: Bitbucket workspace slug
Test file initial content: 'Line 1: UNCHANGED_SECTION_START
Line 2: This is the original text
Line 3: SECTION_TO_UPDATE
Line 4: UNCHANGED_SECTION_END'
OLD marker: 'SECTION_TO_UPDATE'
NEW marker: 'UPDATED_CONTENT'

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call create_branch to create a test branch for isolation | Test branch created successfully |
| 2 | Call create_file on test branch with known multi-section content (has 'SECTION_TO_UPDATE' and 'UNCHANGED_SECTION') | File created successfully with initial content |
| 3 | Call update_file using OLD/NEW marker syntax targeting 'SECTION_TO_UPDATE' text with replacement | update_file returns success response |
| 4 | Call read_file to verify the file content after update | Updated section shows new content, unchanged sections remain exactly as before |
| 5 | LLM validates: only targeted section was modified, other content unchanged, update_file with OLD/NEW markers functioned correctly | Validation confirms precise partial file update with OLD/NEW marker syntax |
| 6 | Cleanup: call delete_branch to remove the test branch | Test branch deleted, repository returned to clean state |

## Expected Final State

Test branch deleted, repository returned to clean state

## Pass/Fail Criteria

PASS: update_file succeeds, read_file shows ONLY the targeted section changed, other content unchanged
FAIL: Update fails, wrong section modified, entire file overwritten, other content changed
