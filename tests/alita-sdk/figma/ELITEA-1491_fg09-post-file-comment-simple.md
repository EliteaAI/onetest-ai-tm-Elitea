---
id: ELITEA-1491
title: "FG09 - Post File Comment (Simple)"
priority: high
type: functional
module: figma
status: ready
execution_type: automated
tags: [post_file_comment, comments, smoke, figma]
requirements: []
---
# ELITEA-1491: FG09 - Post File Comment (Simple)

**Module:** Figma · **Priority:** High · **Type:** Functional

**Objective:** Test posting a basic text comment to a Figma file, verifying the comment is created and a comment ID is returned in the response.

## Preconditions

Figma toolkit is configured and authenticated
FIGMA_TOOLKIT_ID and FIGMA_FILE_KEY env vars are set
Write access to target file for commenting

## Test Data

FIGMA_TOOLKIT_ID: configured Figma toolkit ID
FIGMA_FILE_KEY: valid Figma file key with comment write access
Comment message: "Automated test comment — FG09"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure Figma toolkit with valid API token (account with write access) | Toolkit authenticated with write permissions |
| 2 | Set FIGMA_FILE_KEY to a valid file key the user can comment on | Environment variable set |
| 3 | Invoke post_file_comment tool with file_key and message="Automated test comment — FG09" | POST request sent to Figma comments endpoint |
| 4 | Validate response contains a new comment object with id field | Comment created and ID returned |
| 5 | Verify the comment message in response matches the submitted text | Message content is correct |

## Expected Final State

Message content is correct

## Pass/Fail Criteria

Comment posted successfully with HTTP 200/201 response
Response contains new comment ID
Comment message matches submitted text
Tool completes without error
