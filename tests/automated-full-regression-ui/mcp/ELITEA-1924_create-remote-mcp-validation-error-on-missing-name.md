---
id: ELITEA-1924
title: "Create Remote MCP — Validation Error on Missing Name"
priority: high
type: functional
module: elitea-platform
status: draft
execution_type: manual
tags: [automated:UI:regression]
requirements: []
---

# ELITEA-1924: Create Remote MCP — Validation Error on Missing Name

**Module:** elitea-platform · **Priority:** medium · **Type:** functional

**Objective:** Verify that the Save button remains disabled when only the URL is filled and the Toolkit Name is absent, ensuring the name field is required for MCP creation.

---

## Preconditions

- User is logged in to the Elitea platform.
- User has navigated to the MCP creation page and selected "Remote MCP".

---

## Test Data

| Field | Value |
|-------|-------|
| Toolkit Name | autotest_validation_name |
| URL | https://mcp.example.com/sse |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to MCP creation page and select "Remote MCP" | Form page loads at /app/mcps/create/mcp |
| 2 | Leave "Toolkit Name *" empty | Name field remains empty |
| 3 | Fill "Url *" with "https://mcp.example.com/sse" | Field accepts and displays the URL |
| 4 | Verify Save button remains disabled (name is required to enable save) | Save button is disabled |
| 5 | Fill "Toolkit Name *" with "autotest_validation_name" | Field accepts and displays the input |
| 6 | Verify Save button becomes enabled | Save button is now clickable |
| 7 | Click Save — verify MCP is created | Redirect to MCP detail page occurs |

---

## Expected Final State

The MCP "autotest_validation_name" is successfully created once both required fields are filled.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Save button is disabled until Toolkit Name is provided, and MCP is created after filling both required fields.

**Fail:**
- Any step produces an error or unexpected result.
- Save button is enabled without a Toolkit Name, or MCP creation fails.
