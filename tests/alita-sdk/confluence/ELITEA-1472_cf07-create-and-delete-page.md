---
id: ELITEA-1472
title: "CF07 - Create and Delete Page"
priority: high
type: functional
module: confluence
status: ready
execution_type: automated
tags: [create_page, delete_page, confluence, lifecycle, pages]
requirements: []
---
# ELITEA-1472: CF07 - Create and Delete Page

**Module:** Confluence · **Priority:** High · **Type:** Functional

**Objective:** Verify create_page creates a new page successfully and delete_page removes it, then search_by_title confirms the page no longer exists. Full create-verify-delete lifecycle test.

## Preconditions

Confluence toolkit is configured and authenticated
CF_TOOLKIT_ID, CF_SPACE_KEY, and CF_PARENT_PAGE_ID env vars are set
Write permissions available to create pages in target space

## Test Data

CF_TOOLKIT_ID: Confluence toolkit ID
CF_SPACE_KEY: Confluence space key
CF_PARENT_PAGE_ID: Parent page ID under which test page is created
Test page title: 'Test Page CF07 {timestamp}' (unique per run)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call create_page tool with unique test title (e.g., 'Test Page CF07 {timestamp}') under parent page CF_PARENT_PAGE_ID | Page created successfully, response contains new page ID |
| 2 | LLM validates page creation: page ID returned, title matches, page was created successfully | Creation confirmed with page ID in response |
| 3 | Call delete_page tool with the page ID obtained from creation response | Page deleted without errors |
| 4 | Call search_by_title to search for the deleted page title and verify it no longer appears | Search returns no results for the deleted page title |
| 5 | LLM validates full lifecycle: creation succeeded, deletion succeeded, page no longer findable by title | Validation confirms complete create-delete lifecycle works correctly |

## Expected Final State

Validation confirms complete create-delete lifecycle works correctly

## Pass/Fail Criteria

PASS: Page created successfully with returned page ID, title confirmed, search shows no result after deletion
FAIL: Page creation fails, delete fails, page still findable after deletion
