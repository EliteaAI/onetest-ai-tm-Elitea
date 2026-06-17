---
id: ELITEA-1219
title: "SharePoint Toolkit — MCP-Exposed Tools Operate Correctly with /teams/ Site Path"
priority: high
type: functional
module: sharepoint
status: draft
execution_type: manual
tags: [feat:toolkits, feature:2584, r-2.0.4]
requirements: [EliteaAI/elitea_issues#2584]
---
# ELITEA-1219: SharePoint Toolkit — MCP-Exposed Tools Operate Correctly with /teams/ Site Path

**Module:** Sharepoint · **Priority:** High · **Type:** Functional

**Objective:** Verify that SharePoint tools made available via MCP function correctly against a /teams/ site when Site Path is configured. Covers: MCP toggle enabled; MCP client discovers exposed tools; get_files_list and read_document invoked via MCP return /teams/ data; no site URL resolution errors in MCP responses.

## Preconditions

- Logged in to ELITEA at {{base_url}}
- SharePoint toolkit with Site Path teams/TestTeam, Make tools available by MCP enabled
- An MCP client connected to ELITEA
- /teams/TestTeam site accessible with at least one document

## Test Data

Site Path: teams/TestTeam
Tools to invoke via MCP: get_files_list, read_document
Document path: a valid server-relative path in the /teams/ library

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the SharePoint toolkit. Enable Make tools available by MCP. Set Site Path to teams/TestTeam. Save. | Save completes. No error. MCP toggle is on. |
| 2 | From an MCP client, discover available SharePoint tools. | get_files_list and read_document (and other enabled tools) are listed as available MCP tools. |
| 3 | Invoke get_files_list via MCP. | Files from .../teams/TestTeam are returned. No error in MCP response. |
| 4 | Invoke read_document via MCP with a valid document path. | Document content is returned. No 'site not found' or HTTP error. |

## Expected Final State

Document content is returned. No 'site not found' or HTTP error.

## Pass/Fail Criteria

Pass:
- MCP client discovers the enabled SharePoint tools
- Both get_files_list and read_document return correct data from the /teams/ site via MCP
- No site resolution errors in any MCP response

Fail:
- MCP client does not discover the tools after enabling the toggle
- Any MCP-invoked tool fails or returns data from a wrong site
- 'Site not found' or HTTP error returned via MCP
