---
id: ELITEA-1172
title: "Invalid content_format value rejected at schema level before API call"
priority: medium
type: functional
module: confluence-toolkit-read-page-by-id
status: ready
execution_type: manual
tags: [int:confluence, feat:toolkits, issue:3886, r-2.0.4]
requirements: [EliteaAI/elitea_issues#3886]
---
# ELITEA-1172: Invalid content_format value rejected at schema level before API call

**Module:** Confluence Toolkit Read Page By Id · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that passing an unsupported content_format value is rejected by the Pydantic schema layer before the Confluence API is ever called.

**Coverage:**
- Schema enforces Literal type constraint on content_format
- Unknown values raise validation error
- Confluence API is not called when validation fails
- Error message indicates the invalid value is not in the allowed set

## Preconditions

- Logged in to ELITEA ({{base_url}})
- Confluence toolkit configured with valid credentials

## Test Data

- Page ID: 43679747
- content_format: body.invalid (unsupported value)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call read_page_by_id with page_id=43679747 and content_format=body.invalid | A validation error is returned indicating body.invalid is not an accepted value |
| 2 | Inspect the error message | Error references the allowed values: view, storage, export_view, editor, anonymous, styled_view, atlas_doc_format |
| 3 | Confirm no Confluence API call was made (no page content returned) | No page content appears in the response — Confluence API was not reached |

## Expected Final State

No page content appears in the response — Confluence API was not reached

## Pass/Fail Criteria

**Pass:**
- Validation error raised for unsupported value
- Confluence API not called
- Error message references allowed values

**Fail:**
- Call proceeds with invalid value and reaches Confluence API
- No error returned for clearly invalid value
