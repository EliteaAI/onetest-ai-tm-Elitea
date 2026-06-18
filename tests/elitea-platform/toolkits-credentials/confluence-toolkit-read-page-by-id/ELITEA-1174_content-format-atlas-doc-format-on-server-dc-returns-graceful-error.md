---
id: ELITEA-1174
title: "content_format=atlas_doc_format on Server/DC returns graceful error"
priority: high
type: functional
module: confluence-toolkit-read-page-by-id
status: ready
execution_type: manual
tags: [int:confluence, feat:toolkits, issue:3886, r-2.0.4]
requirements: [EliteaAI/elitea_issues#3886]
---
# ELITEA-1174: content_format=atlas_doc_format on Server/DC returns graceful error

**Module:** Confluence Toolkit Read Page By Id · **Priority:** High · **Type:** Functional

**Objective:** Verify that using atlas_doc_format on a Confluence Server or Data Center instance returns a graceful error — not an unhandled exception — since ADF is Cloud-only.

**Coverage:**
- atlas_doc_format on Server/DC triggers API error
- Error surfaced to user as readable message
- No unhandled Python exception propagated
- Agent session remains usable after failed call

## Preconditions

- Logged in to ELITEA ({{base_url}})
- Connected Confluence instance is Server or Data Center
- Confluence toolkit configured with valid credentials
- A valid page ID exists on the Server/DC instance

## Test Data

- Page ID: [valid page ID on Server/DC instance]
- content_format: atlas_doc_format

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call read_page_by_id with a valid page ID and content_format=atlas_doc_format on a Server/DC Confluence instance | Tool call is accepted at the schema level (atlas_doc_format is a valid value) |
| 2 | Inspect the response | Confluence API returns an error (the body.atlas_doc_format key does not exist on Server/DC); error message is returned to the user |
| 3 | Verify no unhandled Python exception or 500-level internal error is propagated | Error is caught and returned as a readable message, not a stack trace |
| 4 | Send another call to the agent (e.g. a simple read_page_by_id without content_format) | Agent session is still functional; next call succeeds normally |

## Expected Final State

Agent session is still functional; next call succeeds normally

## Pass/Fail Criteria

**Pass:**
- Confluence API error is returned as readable message
- No unhandled exception propagated
- Session remains usable after the failed call

**Fail:**
- Unhandled exception or stack trace surfaced to user
- Agent session becomes unusable after the call
