---
id: ELITEA-1539
title: "JR21 - Get Comments with Image Descriptions (Happy Path)"
priority: medium
type: functional
module: jira
status: ready
execution_type: automated
tags: [get_comments_with_image_descriptions, comments, images, jira]
requirements: []
---
# ELITEA-1539: JR21 - Get Comments with Image Descriptions (Happy Path)

**Module:** Jira · **Priority:** Medium · **Type:** Functional

**Objective:** Verify get_comments_with_image_descriptions retrieves issue comments and includes AI-generated descriptions for any embedded images in the comments.

## Preconditions

JIRA toolkit is configured and authenticated
JIRA_TOOLKIT_NAME env var is set
JIRA_ISSUE_KEY env var set to an issue with comments containing images
Vision-capable model configured

## Test Data

JIRA_TOOLKIT_NAME: name of configured JIRA toolkit
JIRA_ISSUE_KEY: key of issue with comments containing embedded images
Vision model: configured and accessible

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the JIRA toolkit using JIRA_TOOLKIT_NAME env var and valid credentials and a vision-capable model | Toolkit initializes and connects without error |
| 2 | Invoke `get_comments_with_image_descriptions` with JIRA_ISSUE_KEY for an issue whose comments contain embedded images | Tool accepts the parameters and begins execution |
| 3 | Capture the tool response | Response contains comment text with AI-generated descriptions of embedded images |
| 4 | Validate that the LLM confirms image description text is included in the returned comments | LLM confirms image descriptions present in comment content |

## Expected Final State

LLM confirms image descriptions present in comment content

## Pass/Fail Criteria

get_comments_with_image_descriptions returns comments without error
Image descriptions embedded in returned comment text
No exception raised
