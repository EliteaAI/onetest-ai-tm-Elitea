---
id: ELITEA-1927
title: "Edit Remote MCP — Modify Configuration via Raw JSON"
priority: critical
type: functional
module: elitea-platform
status: draft
execution_type: manual
tags: [automated:UI:regression]
requirements: []
---

# ELITEA-1927: Edit Remote MCP — Modify Configuration via Raw JSON

**Module:** elitea-platform · **Priority:** medium · **Type:** functional

**Objective:** Verify that a Remote MCP's configuration can be edited directly through the Raw JSON view, and that changes are reflected in the Form view and persisted after a page reload.

---

## Preconditions

- User is logged in to the Elitea platform.
- An existing Remote MCP is available and open on its detail page.

---

## Test Data

| Field | Value |
|-------|-------|
| Updated Description | Updated via raw JSON |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open an existing Remote MCP detail page | Detail page loads |
| 2 | Click "Raw Json" toggle button — verify JSON editor appears | JSON editor is visible |
| 3 | Verify JSON contains current config (name, description, settings with url, timeout, cache_ttl, ssl_verify, enable_caching, selected_tools, available_mcp_tools) | All expected fields are present in the JSON |
| 4 | Modify "description" value in JSON editor to "Updated via raw JSON" | JSON editor reflects the change |
| 5 | Verify Save button becomes enabled | Save button is clickable |
| 6 | Click Save | Operation completes successfully |
| 7 | Click "Form" toggle button — verify Description field shows "Updated via raw JSON" | Form view reflects the updated description |
| 8 | Reload page — verify change persisted in both Form and Raw Json views | Both views show "Updated via raw JSON" after reload |

---

## Expected Final State

The description change made via Raw JSON is visible in the Form view and persists after a page reload.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- JSON edit is reflected in Form view and persists after reload.

**Fail:**
- Any step produces an error or unexpected result.
- JSON change is not reflected in Form view or not persisted.
