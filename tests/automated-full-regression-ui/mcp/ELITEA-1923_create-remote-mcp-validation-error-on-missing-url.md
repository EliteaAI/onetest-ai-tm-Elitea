---
id: ELITEA-1923
title: "Create Remote MCP — Validation Error on Missing URL"
priority: medium
type: functional
module: elitea-platform
status: draft
execution_type: automated
tags: [automated:UI:regression]
requirements: []
---

# ELITEA-1923: Create Remote MCP — Validation Error on Missing URL

**Module:** elitea-platform · **Priority:** medium · **Type:** functional

**Objective:** Verify that attempting to save a Remote MCP without a URL triggers a validation error, prevents creation, and allows recovery by providing the missing URL.

---

## Preconditions

- User is logged in to the Elitea platform.
- User has navigated to the MCP creation page and selected "Remote MCP".

---

## Test Data

| Field | Value |
|-------|-------|
| Toolkit Name | autotest_validation_no_url |
| URL (recovery) | https://mcp.example.com/sse |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to MCP creation page and select "Remote MCP" | Form page loads at /app/mcps/create/mcp |
| 2 | Fill "Toolkit Name *" with "autotest_validation_no_url" | Field accepts and displays the input |
| 3 | Leave "Url *" field empty | URL field remains empty |
| 4 | Verify Save button becomes enabled (name alone enables it) | Save button is clickable |
| 5 | Click Save | Save is attempted |
| 6 | Verify validation error message "Field is required" appears below the Url field | Error message is displayed under the URL field |
| 7 | Verify MCP is NOT created (stays on create page) | Page remains on /app/mcps/create/mcp |
| 8 | Fill "Url *" with "https://mcp.example.com/sse" | Field accepts and displays the URL |
| 9 | Click Save again — verify MCP is created successfully | Redirect to MCP detail page occurs |

---

## Expected Final State

The MCP "autotest_validation_no_url" is created successfully after providing the URL; the validation error is no longer shown.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Validation error "Field is required" appears when URL is missing, and creation succeeds after supplying the URL.

**Fail:**
- Any step produces an error or unexpected result.
- MCP is created without a URL, or the validation error is not shown.
