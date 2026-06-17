---
id: ELITEA-1179
title: "Default (no content_format): read_page_by_id returns toolkit-level format"
priority: critical
type: functional
module: confluence-toolkit-read-page-by-id
status: ready
execution_type: manual
tags: [int:confluence, feat:toolkits, issue:3886, r-2.0.4]
requirements: [EliteaAI/elitea_issues#3886]
---
# ELITEA-1179: Default (no content_format): read_page_by_id returns toolkit-level format

**Module:** Confluence Toolkit Read Page By Id · **Priority:** Critical · **Type:** Functional

**Objective:** Verify backward compatibility — calling read_page_by_id without content_format uses the toolkit-level default format and returns page content correctly.

**Coverage:**
- Default format passthrough (no override)
- Response contains page id, title, and non-empty body
- No errors on call without optional parameter

## Preconditions

- Logged in to ELITEA ({{base_url}})
- Confluence toolkit configured with valid token and toolkit-level content_format set to view
- Test agent available: {{base_url}}
- Page ID 43679747 exists in the connected Confluence space

## Test Data

- Page ID: 43679747
- Confluence space: SD
- content_format: not provided

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the Confluence-connected agent at https://dev.elitea.ai/app/406/agents/all/699/1262 | Agent chat interface opens and is ready to accept input |
| 2 | Call read_page_by_id with page_id=43679747 and no content_format parameter | Tool call is accepted without validation error |
| 3 | Inspect the response | Response contains page id 43679747, a title, and non-empty body content in view (HTML) format |
| 4 | Verify no error message is returned | No error or exception is present in the response |

## Expected Final State

No error or exception is present in the response

## Pass/Fail Criteria

**Pass:**
- Response includes page id, title, and non-empty body
- Format matches toolkit-level default (view)
- No error returned

**Fail:**
- Response is empty or missing body content
- Error returned on a valid call without content_format
