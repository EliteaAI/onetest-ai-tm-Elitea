---
id: ELITEA-1175
title: "content_format=atlas_doc_format returns raw ADF JSON verbatim (Confluence Cloud only)"
priority: high
type: functional
module: confluence-toolkit-read-page-by-id
status: ready
execution_type: manual
tags: [int:confluence, feat:toolkits, issue:3886, r-2.0.4]
requirements: [EliteaAI/elitea_issues#3886]
---
# ELITEA-1175: content_format=atlas_doc_format returns raw ADF JSON verbatim (Confluence Cloud only)

**Module:** Confluence Toolkit Read Page By Id · **Priority:** High · **Type:** Functional

**Objective:** Verify that atlas_doc_format returns the page as raw Atlassian Document Format (ADF) JSON without HTML-stripping or markdownification — Cloud only.

**Coverage:**
- atlas_doc_format accepted as valid content_format
- expand body.atlas_doc_format,version sent to Confluence API
- ADF JSON returned verbatim (not processed through markdownify or BeautifulSoup)
- JSON structure preserved (version, type:doc, content array)

## Preconditions

- Logged in to ELITEA ({{base_url}})
- Connected Confluence instance is Cloud (not Server/Data Center)
- Confluence toolkit configured with valid credentials
- Page ID 43679747 exists

## Test Data

- Page ID: 43679747
- content_format: atlas_doc_format
- Expected response prefix: {"version":1,"type":"doc"...

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call read_page_by_id with page_id=43679747 and content_format=atlas_doc_format on a Confluence Cloud instance | Tool call is accepted without validation error |
| 2 | Inspect the response | Response starts with ADF JSON root structure (e.g. {"version":1,"type":"doc") |
| 3 | Verify the JSON is returned verbatim — not HTML-stripped | JSON keys and curly braces are intact; content is not mangled by markdownify or BeautifulSoup |
| 4 | Verify no error is returned | No error or exception in the response |

## Expected Final State

No error or exception in the response

## Pass/Fail Criteria

**Pass:**
- Response is valid ADF JSON starting with {\"version\":1,\"type\":\"doc\"
- JSON structure intact (not HTML-stripped)
- No error returned

**Fail:**
- Response is empty, HTML, or mangled JSON
- Error returned on Cloud instance
