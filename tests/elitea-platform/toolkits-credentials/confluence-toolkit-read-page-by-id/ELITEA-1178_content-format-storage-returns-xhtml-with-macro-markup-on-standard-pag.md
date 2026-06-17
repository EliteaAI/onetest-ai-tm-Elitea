---
id: ELITEA-1178
title: "content_format=storage returns XHTML with macro markup on standard page"
priority: critical
type: functional
module: confluence-toolkit-read-page-by-id
status: ready
execution_type: manual
tags: [int:confluence, feat:toolkits, issue:3886, r-2.0.4]
requirements: [EliteaAI/elitea_issues#3886]
---
# ELITEA-1178: content_format=storage returns XHTML with macro markup on standard page

**Module:** Confluence Toolkit Read Page By Id · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that passing content_format=storage to read_page_by_id causes the Confluence API to return the raw XHTML storage format with macro markup preserved.

**Coverage:**
- content_format=storage accepted and forwarded
- Response body contains Confluence XHTML storage XML
- expand sent to Confluence API is body.storage,version

## Preconditions

- Logged in to ELITEA ({{base_url}})
- Confluence toolkit configured with valid credentials
- Page ID 43679747 exists and contains content

## Test Data

- Page ID: 43679747
- content_format: storage

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the Confluence-connected agent at https://dev.elitea.ai/app/406/agents/all/699/1262 | Agent chat interface is ready |
| 2 | Call read_page_by_id with page_id=43679747 and content_format=storage | Tool call is accepted without validation error |
| 3 | Inspect the response body | Response body contains Confluence XHTML storage XML markup (e.g. <ac: tags, <ri: tags, or raw HTML storage format) |
| 4 | Confirm response is non-empty and contains the page id | Page id 43679747 and title are present; body is non-empty |

## Expected Final State

Page id 43679747 and title are present; body is non-empty

## Pass/Fail Criteria

**Pass:**
- Response contains XHTML storage XML
- Page id and title present
- No error returned

**Fail:**
- Response is empty or in view HTML format instead of storage
- Error returned
