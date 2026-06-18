---
id: ELITEA-1493
title: "FG10 - Post File Comment with Position"
priority: medium
type: functional
module: figma
status: ready
execution_type: automated
tags: [post_file_comment, position, comments, vector, figma]
requirements: []
---
# ELITEA-1493: FG10 - Post File Comment with Position

**Module:** Figma · **Priority:** Medium · **Type:** Functional

**Objective:** Test posting a comment with Vector positioning metadata (x/y coordinates on the canvas), verifying the comment is anchored to a specific position in the file.

## Preconditions

Figma toolkit is configured and authenticated
FIGMA_TOOLKIT_ID and FIGMA_FILE_KEY env vars are set
Write access to target file for commenting
Vector position coordinates available

## Test Data

FIGMA_TOOLKIT_ID: configured Figma toolkit ID
FIGMA_FILE_KEY: valid Figma file key
Comment message: "Positioned test comment — FG10"
client_meta: {"node_id": "", "node_offset": {"x": 100, "y": 200}}

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure Figma toolkit with valid API token (account with write access) | Toolkit authenticated with write permissions |
| 2 | Set FIGMA_FILE_KEY to a valid file key | Environment variable set |
| 3 | Invoke post_file_comment with message text and client_meta containing Vector position {"x": 100, "y": 200} | POST request sent with position payload |
| 4 | Validate response contains new comment ID | Comment created successfully |
| 5 | Verify response includes positional metadata anchoring comment to canvas coordinates | client_meta or position data present in comment response |

## Expected Final State

client_meta or position data present in comment response

## Pass/Fail Criteria

Positioned comment posted successfully
Response contains new comment ID
Comment includes client_meta/position anchor data
Tool completes without error
