---
id: ELITEA-1171
title: "content_format parameter visible with correct description in ELITEA Confluence toolkit UI"
priority: medium
type: functional
module: confluence-toolkit-read-page-by-id
status: ready
execution_type: manual
tags: [int:confluence, feat:toolkits, issue:3886, r-2.0.4]
requirements: [EliteaAI/elitea_issues#3886]
---
# ELITEA-1171: content_format parameter visible with correct description in ELITEA Confluence toolkit UI

**Module:** Confluence Toolkit Read Page By Id · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that the content_format parameter is discoverable in the ELITEA toolkit configuration UI with an accurate description listing supported values and their use cases.

**Coverage:**
- content_format appears as optional parameter for read_page_by_id
- Parameter description mentions storage and structured macro use case
- Allowed values include: view, storage, export_view, editor, anonymous, styled_view, atlas_doc_format
- Default is shown as toolkit setting (not hardcoded)

## Preconditions

- Logged in to ELITEA ({{base_url}})
- Confluence toolkit exists and is configured

## Test Data

- Navigation path: Toolkits → Confluence → read_page_by_id tool

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Toolkits in ELITEA and open the Confluence toolkit configuration | Confluence toolkit configuration page is displayed |
| 2 | Locate the read_page_by_id tool and expand its parameter list | Parameter list for read_page_by_id is visible |
| 3 | Find the content_format parameter in the list | content_format appears as an optional parameter |
| 4 | Read the parameter description | Description mentions: override toolkit-level format, use storage for structured macros (rw-ui-tabs-macro), styled_view for export-styled HTML, atlas_doc_format for Cloud ADF JSON |
| 5 | Verify allowed values shown in the UI | Dropdown or description includes: view, storage, export_view, editor, anonymous, styled_view, atlas_doc_format |

## Expected Final State

Dropdown or description includes: view, storage, export_view, editor, anonymous, styled_view, atlas_doc_format

## Pass/Fail Criteria

**Pass:**
- content_format parameter is visible in the tool parameter list
- Description accurately describes the values and their use cases
- All 7 allowed values are present

**Fail:**
- content_format parameter is not visible in the UI
- Description is missing or inaccurate
