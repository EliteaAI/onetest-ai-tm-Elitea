---
id: ELITEA-4521
title: "Verify each of the four Tavily tools can be run individually from the toolkit Test page with correct parameter fields"
priority: critical
type: functional
module: tavily-toolkit
status: draft
execution_type: manual
tags: [feat:admin-platform, feat:chat, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6981]
---

## Preconditions

- A Tavily toolkit with a valid API key and all four tools selected, open on its "Test Toolkit" page

## Test Data

| Tool | Expected Fields |
|------|------------------|
| Web search | Query (required), Search Depth, Topic, Time Range |
| Web extract | Urls (required, JSON array) |
| Web crawl | Url (required), Instructions, Max Depth (default 1), Limit (default 10) |
| Web map | Url (required), Instructions, Max Depth (default 1), Limit (default 20) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Select "Web search" from the Tool dropdown | Only Query, Search Depth, Topic, Time Range fields are shown; no URL-related fields |
| 2 | Select "Web extract" | Only the Urls field is shown; no Query/Search Depth/Topic/Time Range fields |
| 3 | Select "Web crawl" | Url, Instructions, Max Depth (default 1), Limit (default 10) are shown |
| 4 | Select "Web map" | Url, Instructions, Max Depth (default 1), Limit (default 20) are shown |
| 5 | Run a valid test for each of the four tools with reasonable input | Each shows a successful, readable result in the "Results" panel |
| 6 | Switch between tools in the dropdown (e.g. from Web search with a Query filled, to Web extract) | Fields reset/clear appropriately; no leftover value bleeds into a field that does not apply to the newly selected tool |

## Expected Final State

Each tool's Test page correctly exposes only its own relevant parameter fields.

## Pass/Fail Criteria

**Pass:**
- Each tool shows exactly its documented fields
- Each runs successfully
- Switching tools clears irrelevant leftover values

**Fail:**
- A tool shows fields that do not belong to it
- A tool fails to run
- A leftover value from a previously selected tool persists
