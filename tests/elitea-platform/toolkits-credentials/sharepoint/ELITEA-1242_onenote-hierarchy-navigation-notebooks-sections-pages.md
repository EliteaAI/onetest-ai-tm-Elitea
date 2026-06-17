---
id: ELITEA-1242
title: "OneNote hierarchy navigation: notebooks → sections → pages"
priority: high
type: functional
module: sharepoint
status: ready
execution_type: manual
tags: [feat:toolkits, issue:2355, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#2355]
---
# ELITEA-1242: OneNote hierarchy navigation: notebooks → sections → pages

**Module:** Sharepoint · **Priority:** High · **Type:** Functional

**Objective:** Verify that the OneNote hierarchy can be navigated from notebooks to sections to pages, that `select` field filtering works correctly, and that including the forbidden `contentUrl` field in `select` is handled as documented.

**Coverage:**
- `onenote_get_notebooks` returns all notebooks with default fields
- `onenote_get_sections` returns all sections for a notebook
- `onenote_get_pages` lists pages with default and custom `select` fields
- `select` parameter returns only specified fields when valid fields provided; returns all default fields when no valid fields provided
- `contentUrl` in `select` causes Graph API 400 error

## Preconditions

- SharePoint toolkit configured with Delegated OAuth auth
- SharePoint site has at least one notebook with 2+ sections, each containing pages

## Test Data

- Notebook ID: [from onenote_get_notebooks]
- Section ID: [from onenote_get_sections]

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Agent with SharePoint toolkit. Invoke `Onenote get notebooks`. | All OneNote notebooks on the SharePoint site returned with id, displayName, createdDateTime, lastModifiedDateTime, isDefault, isShared, and links.oneNoteWebUrl. |
| 2 | Invoke `Onenote get sections` providing the target notebook_id. | All sections within the notebook listed with id, displayName, createdDateTime, lastModifiedDateTime, pagesUrl, isDefault. |
| 3 | Invoke `Onenote get pages` providing a valid section_id. | All pages within the section returned with id, title, createdDateTime, lastModifiedDateTime. |
| 4 | Invoke `Onenote get pages` with select=["id", "title"]. | Only the specified fields (id and title) are returned per page. If no recognized fields are passed, all default fields are returned. |
| 5 | Invoke `Onenote get pages` with select including contentUrl (e.g. select=["id", "title", "contentUrl"]). | Graph API 400 error is returned — contentUrl is not allowed in the select parameter for this endpoint. |

## Expected Final State

Graph API 400 error is returned — contentUrl is not allowed in the select parameter for this endpoint.

## Pass/Fail Criteria

**Pass:**
- Full hierarchy navigable; default fields returned correctly
- `select` filtering returns only specified fields; no recognized fields returns defaults
- `contentUrl` in `select` returns 400

**Fail:**
- Empty results when data exists
- Invalid field causes silent failure instead of 400
