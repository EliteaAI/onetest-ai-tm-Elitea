---
id: ELITEA-1176
title: "content_format=styled_view returns HTML with inline CSS"
priority: high
type: functional
module: confluence-toolkit-read-page-by-id
status: ready
execution_type: manual
tags: [int:confluence, feat:toolkits, issue:3886, r-2.0.4]
requirements: [EliteaAI/elitea_issues#3886]
---
# ELITEA-1176: content_format=styled_view returns HTML with inline CSS

**Module:** Confluence Toolkit Read Page By Id · **Priority:** High · **Type:** Functional

**Objective:** Verify that content_format=styled_view returns export-styled HTML with inline CSS via the _StyledView shim.

**Coverage:**
- styled_view accepted as valid content_format value
- expand body.styled_view,version sent to Confluence API
- Response is non-empty HTML with inline CSS styling

## Preconditions

- Logged in to ELITEA ({{base_url}})
- Confluence toolkit configured with valid credentials
- Page ID 43679747 exists

## Test Data

- Page ID: 43679747
- content_format: styled_view

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call read_page_by_id with page_id=43679747 and content_format=styled_view | Tool call is accepted without validation error |
| 2 | Inspect the response body | Response body is non-empty HTML content with inline CSS styling (style= attributes visible in HTML tags) |
| 3 | Verify no error is returned | No error or exception in the response |

## Expected Final State

No error or exception in the response

## Pass/Fail Criteria

**Pass:**
- Response is non-empty HTML with inline CSS
- No error returned

**Fail:**
- Response is empty or in plain view HTML without inline CSS
- Validation error raised for styled_view value
