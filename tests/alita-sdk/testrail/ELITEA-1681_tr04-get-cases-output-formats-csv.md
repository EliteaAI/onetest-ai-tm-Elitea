---
id: ELITEA-1681
title: "TR04 - Get Cases Output Formats (CSV)"
priority: medium
type: functional
module: testrail
status: ready
execution_type: automated
tags: [output-format, get_cases, testrail, csv]
requirements: []
---
# ELITEA-1681: TR04 - Get Cases Output Formats (CSV)

**Module:** Testrail · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the get_cases tool supports multiple output formats, specifically CSV. Tests output format flexibility when retrieving test cases.

## Preconditions

TestRail toolkit is configured and authenticated
TESTRAIL_TOOLKIT_NAME, TESTRAIL_TOOLKIT_ID, and TESTRAIL_PROJECT_ID env vars are set
Project has at least one test case

## Test Data

TESTRAIL_TOOLKIT_NAME: name of configured TestRail toolkit
TESTRAIL_TOOLKIT_ID: ID of the toolkit configuration
TESTRAIL_PROJECT_ID: ID of an existing TestRail project
output_format: csv

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the TestRail toolkit using TESTRAIL_TOOLKIT_NAME and valid credentials | Toolkit initializes without error |
| 2 | Invoke get_cases with project_id=TESTRAIL_PROJECT_ID and output_format='csv' | Tool call is accepted and executes |
| 3 | Capture the tool response string | Response is a non-empty string |
| 4 | Validate the response is properly CSV-formatted with a header row (e.g. 'title,id') and at least one data row with comma-separated values | Response contains CSV structure: header row present, data rows with commas and newlines, no errors |

## Expected Final State

Response contains CSV structure: header row present, data rows with commas and newlines, no errors

## Pass/Fail Criteria

Tool executes successfully with csv output format
Response is a string containing CSV data
First row is a header (e.g. title,id)
At least one data row is present
Rows are separated by newlines
No errors or exceptions
