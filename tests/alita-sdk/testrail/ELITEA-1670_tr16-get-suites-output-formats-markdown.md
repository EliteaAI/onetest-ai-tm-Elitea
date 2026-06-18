---
id: ELITEA-1670
title: "TR16 - Get Suites Output Formats (Markdown)"
priority: medium
type: functional
module: testrail
status: ready
execution_type: automated
tags: [output-format, get_suites, markdown, testrail]
requirements: []
---
# ELITEA-1670: TR16 - Get Suites Output Formats (Markdown)

**Module:** Testrail · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the get_suites tool supports multiple output formats, specifically markdown. Tests output format flexibility for suite listing.

## Preconditions

TestRail toolkit is configured and authenticated
TESTRAIL_TOOLKIT_NAME, TESTRAIL_TOOLKIT_ID, and TESTRAIL_PROJECT_ID env vars are set
Project has at least one test suite

## Test Data

TESTRAIL_TOOLKIT_NAME: name of configured TestRail toolkit
TESTRAIL_PROJECT_ID: ID of an existing TestRail project
output_format: markdown

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the TestRail toolkit using TESTRAIL_TOOLKIT_NAME and valid credentials | Toolkit initializes without error |
| 2 | Invoke get_suites with project_id=TESTRAIL_PROJECT_ID and output_format='markdown' | Tool call is accepted and executes |
| 3 | Capture the tool response string | Response is a non-empty string |
| 4 | Validate the response is properly markdown-formatted, containing suite names and IDs in table or list structure with markdown syntax | Response contains markdown structure (pipes, headers, or list items); suite names and IDs are present; no errors |

## Expected Final State

Response contains markdown structure (pipes, headers, or list items); suite names and IDs are present; no errors

## Pass/Fail Criteria

Tool executes successfully with markdown output format
Response is a string containing markdown-formatted data
Markdown structure is present (e.g. table headers with pipes, or list formatting)
Suite data (names, IDs) is visible in the output
No errors or exceptions
