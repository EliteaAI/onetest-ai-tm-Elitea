---
id: ELITEA-1922
title: "Create Remote MCP — All Fields Populated"
priority: critical
type: functional
module: elitea-platform
status: ready
execution_type: automated
automation_test_id: tests.ui.toolkits.test_mcp_create_remote.test_create_remote_mcp_all_fields_populated
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/292
tags: [automated:UI:regression]
requirements: []
---

# ELITEA-1922: Create Remote MCP — All Fields Populated

**Module:** elitea-platform · **Priority:** medium · **Type:** functional

**Objective:** Verify that a Remote MCP can be created with all available configuration fields filled in, and that all values are persisted and visible in both Form and Raw JSON views.

---

## Preconditions

- User is logged in to the Elitea platform.
- User has navigated to the MCP creation page and selected "Remote MCP".

---

## Test Data

| Field | Value |
|-------|-------|
| Toolkit Name | autotest_remote_mcp_full |
| Description | Full configuration test MCP |
| URL | https://mcp.example.com/sse |
| Headers JSON | {"Authorization": "Bearer test123"} |
| Client Id | test_client_id |
| Client Secret | test_secret_value |
| Scopes | read,write |
| Timeout | 600 |
| Cache TTL | 120 |
| Enable Caching | checked (default) |
| Ssl Verify | unchecked |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to MCP creation page (/app/mcps/create) and select "Remote MCP" | Form page loads at /app/mcps/create/mcp |
| 2 | Fill "Toolkit Name *" with "autotest_remote_mcp_full" | Field accepts and displays the input |
| 3 | Fill "Description" with "Full configuration test MCP" | Field accepts and displays the input |
| 4 | Fill "Url *" with "https://mcp.example.com/sse" | Field accepts and displays the URL |
| 5 | Expand "Headers" section — enter JSON: {"Authorization": "Bearer test123"} | Headers JSON editor accepts the input |
| 6 | Fill "Client Id" with "test_client_id" | Field accepts and displays the input |
| 7 | Fill "Client Secret" field (Password view active by default) with "test_secret_value" | Field accepts masked input |
| 8 | Fill "Scopes" with "read,write" | Field accepts and displays the input |
| 9 | Change "Timeout" from default 300 to 600 | Timeout field updates to 600 |
| 10 | Verify "Enable Caching" checkbox is checked by default | Checkbox is checked |
| 11 | Change "Cache TTL" from 300 to 120 | Cache TTL field updates to 120 |
| 12 | Verify "Ssl Verify" checkbox is checked by default — uncheck it | Ssl Verify checkbox becomes unchecked |
| 13 | Click Save | Operation completes successfully; MCP detail page loads |
| 14 | Verify MCP is created and detail page loads | Detail page is accessible with correct name |
| 15 | Switch to "Raw Json" view — verify JSON contains all configured values | JSON shows name, description, url, timeout:600, cache_ttl:120, ssl_verify:false, enable_caching:true |

---

## Expected Final State

The MCP "autotest_remote_mcp_full" is created with all fields persisted; the Raw JSON view reflects every configured value accurately.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- All configured values are correctly reflected in both Form and Raw JSON views.

**Fail:**
- Any step produces an error or unexpected result.
- One or more configured values are missing or incorrect in the saved MCP.
