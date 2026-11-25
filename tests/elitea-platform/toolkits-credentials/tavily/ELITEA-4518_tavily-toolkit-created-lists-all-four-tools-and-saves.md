---
id: ELITEA-4518
title: "Verify a Tavily toolkit can be created, lists all four tools, and saves successfully"
priority: critical
type: functional
module: tavily-toolkit
status: draft
execution_type: manual
tags: [feat:admin-platform, feat:chat, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6981]
---

## Preconditions

- User is logged in to `{{base_url}}` with access to create toolkits in a project; a valid `tavily` credential already exists

## Test Data

| Field | Value |
|-------|-------|
| Toolkit type | Tavily (category "Other") |
| Settings | Max Results (5), Max Search Depth (basic), Extract Depth (basic), Max Page Chars (20000), Allowed/Blocked Domains, Per Run Call Cap (10) |
| Tools | web_search, web_extract, web_crawl, web_map |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Go to Toolkits & Indexes → "+ Toolkit" → search "Tavily" → select it | "New Tavily Toolkit" form opens with the Configuration section showing the settings listed above with their documented defaults |
| 2 | Inspect the Tools section | All four tools (Web search, Web extract, Web crawl, Web map) are listed and selected by default |
| 3 | Enter a toolkit name, select the credential, keep defaults, save | Toolkit saves without error |
| 4 | Reopen the toolkit | Name, credential, and settings match what was configured |
| 5 | Reopen the toolkit, deselect Web crawl and Web map, save, reload | Only the remaining selected tools are retained after reload |

## Expected Final State

A Tavily toolkit with configurable tool selection and default settings exists and persists correctly.

## Pass/Fail Criteria

**Pass:**
- All four tools are listed and selectable
- Defaults match documentation
- Settings and tool selection persist after save/reload

**Fail:**
- A tool is missing from the list
- A default is wrong
- Settings/tool selection do not persist
