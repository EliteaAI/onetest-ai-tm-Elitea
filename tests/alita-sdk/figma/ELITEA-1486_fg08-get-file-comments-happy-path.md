---
id: ELITEA-1486
title: "FG08 - Get File Comments (Happy Path)"
priority: high
type: functional
module: figma
status: ready
execution_type: automated
tags: [get_file_comments, comments, smoke, figma]
requirements: []
---
# ELITEA-1486: FG08 - Get File Comments (Happy Path)

**Module:** Figma · **Priority:** High · **Type:** Functional

**Objective:** Verify get_file_comments retrieves all comments from a Figma file, returning a list of comments with author, message, and positional data.

## Preconditions

Figma toolkit is configured and authenticated
FIGMA_TOOLKIT_ID and FIGMA_FILE_KEY env vars are set
Target file has at least one comment

## Test Data

FIGMA_TOOLKIT_ID: configured Figma toolkit ID
FIGMA_FILE_KEY: valid Figma file key for a file with existing comments

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure Figma toolkit with valid API token | Toolkit authenticated |
| 2 | Set FIGMA_FILE_KEY to a file that has at least one comment | Environment variable set |
| 3 | Invoke get_file_comments tool with file_key parameter | API request sent to Figma comments endpoint |
| 4 | Validate response contains comments array | Comments list is present in response |
| 5 | Verify each comment has id, message, created_at, and user fields | Comment data is complete and structured |
| 6 | Confirm at least one comment is returned | File has accessible comments |

## Expected Final State

File has accessible comments

## Pass/Fail Criteria

Comments list returned successfully with at least one comment
Each comment has id, message, and created_at fields
Author information included in each comment
Tool completes without error
