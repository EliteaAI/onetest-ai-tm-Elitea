---
id: ELITEA-1249
title: "Tool input validation for OneNote tools"
priority: high
type: functional
module: sharepoint
status: ready
execution_type: manual
tags: [feat:toolkits, issue:2355, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#2355]
---
# ELITEA-1249: Tool input validation for OneNote tools

**Module:** Sharepoint · **Priority:** High · **Type:** Functional

**Objective:** Verify that OneNote tools return clear descriptive errors for invalid inputs, and that edge cases like the forbidden contentUrl select field and missing title tag in page creation behave as documented.

**Coverage:**
- Invalid notebook/section/page IDs return descriptive errors
- contentUrl in select is silently ignored — only allowed fields returned
- onenote_create_page with HTML missing title tag creates page with empty title
- Missing required section_id returns validation error
- Invalid page_id on delete returns clear error

## Preconditions

- Agent with SharePoint toolkit (Delegated OAuth auth)

## Test Data

- Invalid notebook ID: non-existent-id-12345
- Invalid section ID: non-existent-section
- Invalid page ID: non-existent-page
- Page HTML without title tag: <html><body><p>No title here</p></body></html>
- select with forbidden field: ["id", "title", "contentUrl"]

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Invoke `Onenote get sections` with invalid notebook_id. | Clear descriptive error returned (e.g. "Notebook not found"). No crash or unhandled exception. |
| 2 | Invoke `Onenote get pages` with invalid section_id. | Clear descriptive error returned. |
| 3 | Invoke `Onenote get pages` with select=["id", "title", "contentUrl"]. | API silently ignores the forbidden contentUrl field and returns only the allowed fields (id, title). |
| 4 | Invoke `Onenote read page` with invalid page_id. | Clear descriptive error returned. |
| 5 | Invoke `Onenote create page` with HTML that has no <title> tag. | API creates the page with an empty title string. Page is successfully created. |
| 6 | Invoke `Onenote create page` omitting the required section_id. | Validation error returned indicating the required field is missing. Page is not created. |
| 7 | Invoke `Onenote delete page` with invalid page_id. | Clear descriptive error returned — no silent failure. |

## Expected Final State

Clear descriptive error returned — no silent failure.

## Pass/Fail Criteria

**Pass:**
- Invalid IDs produce clear descriptive errors
- contentUrl in select silently ignored; only allowed fields returned
- Missing title tag creates page with empty title string
- Missing section_id returns validation error

**Fail:**
- Invalid inputs cause generic errors or unhandled exceptions
- contentUrl causes 400 or crash
- Missing title tag blocks page creation unexpectedly
