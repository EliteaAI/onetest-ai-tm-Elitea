---
id: ELITEA-1177
title: "content_format=storage resolves empty body on rw-ui-tabs-macro page (core bug fix)"
priority: critical
type: functional
module: confluence-toolkit-read-page-by-id
status: ready
execution_type: manual
tags: [int:confluence, feat:toolkits, issue:3886, r-2.0.4]
requirements: [EliteaAI/elitea_issues#3886]
---
# ELITEA-1177: content_format=storage resolves empty body on rw-ui-tabs-macro page (core bug fix)

**Module:** Confluence Toolkit Read Page By Id · **Priority:** Critical · **Type:** Functional

**Objective:** Verify the core bug fix — pages using rw-ui-tabs-macro that return empty body with the default view format now return full content when content_format=storage is specified.

**Coverage:**
- Default view format returns empty/incomplete body for macro-based pages (known limitation)
- content_format=storage returns non-empty body for the same page
- Response body contains ac:structured-macro tags in storage format

## Preconditions

- Logged in to ELITEA ({{base_url}})
- Confluence toolkit configured with valid credentials
- A Confluence page exists that uses the rw-ui-tabs-macro structured macro
- Page ID of the macro-based page is known (confirm with team)

## Test Data

- Page ID: [macro-based page ID — confirm with team]
- Confluence space: SD
- content_format step 1: not provided (default)
- content_format step 2: storage

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call read_page_by_id with the macro page ID and no content_format parameter | Response is returned without error; body content is empty or significantly incomplete (macro not rendered) |
| 2 | Call read_page_by_id again with the same macro page ID and content_format=storage | Tool call is accepted without error |
| 3 | Inspect the response body from step 2 | Response body is non-empty and contains ac:structured-macro tag(s) in storage XML format |
| 4 | Compare the two responses side by side | Step 1 body is empty/incomplete; step 2 body contains full macro content — confirming the fix works |

## Expected Final State

Step 1 body is empty/incomplete; step 2 body contains full macro content — confirming the fix works

## Pass/Fail Criteria

**Pass:**
- Default view returns empty or incomplete body for macro page
- storage format returns full non-empty body with structured macro tags
- No errors on either call

**Fail:**
- storage format also returns empty body
- Error returned on either call
