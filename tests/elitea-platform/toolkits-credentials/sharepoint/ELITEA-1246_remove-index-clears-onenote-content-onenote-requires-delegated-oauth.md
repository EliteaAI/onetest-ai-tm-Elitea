---
id: ELITEA-1246
title: "Remove index clears OneNote content; OneNote requires Delegated OAuth"
priority: medium
type: functional
module: sharepoint
status: ready
execution_type: manual
tags: [feat:toolkits, issue:2355, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#2355]
---
# ELITEA-1246: Remove index clears OneNote content; OneNote requires Delegated OAuth

**Module:** Sharepoint · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that Remove index clears previously indexed OneNote content, and that OneNote tools are not available in App Credentials (REST API) auth mode.

**Coverage:**
- Remove index removes all indexed OneNote content
- Search index returns no results after removal
- OneNote tools fail with clear auth error when toolkit uses App Credentials mode

## Preconditions

- OneNote content previously indexed via Index data
- A second SharePoint toolkit configured with App Credentials (client_id + client_secret) auth mode available

## Test Data

- Keyword previously returning OneNote results: [keyword1]
- Second toolkit: configured with App Credentials (REST API) mode

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Invoke `Remove index`. | Indexed content removed; success confirmation returned. |
| 2 | Invoke `Search index` with [keyword1]. | No results returned — indexed OneNote content is cleared. |
| 3 | Open the SharePoint toolkit configured with App Credentials (REST API) auth. Attempt to invoke onenote_get_notebooks. | A clear error is returned indicating OneNote tools require Delegated OAuth (Graph API) and are not available in App Credentials mode. |

## Expected Final State

A clear error is returned indicating OneNote tools require Delegated OAuth (Graph API) and are not available in App Credentials mode.

## Pass/Fail Criteria

**Pass:**
- Remove index clears all indexed content; search returns no results after removal
- OneNote tools fail with clear auth error in App Credentials mode

**Fail:**
- Indexed content still searchable after removal
- OneNote tools silently succeed in App Credentials mode
