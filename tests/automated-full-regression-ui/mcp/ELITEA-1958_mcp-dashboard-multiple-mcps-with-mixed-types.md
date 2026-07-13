---
id: ELITEA-1958
title: "MCP Dashboard — Multiple MCPs with Mixed Types"
priority: medium
type: functional
module: elitea-platform
status: draft
execution_type: manual
tags: [automated:UI:regression]
requirements: []
---

# ELITEA-1958: MCP Dashboard — Multiple MCPs with Mixed Types

**Module:** elitea-platform · **Priority:** medium · **Type:** functional

**Objective:** Verify that the MCP list correctly displays both Local and Remote MCPs with accurate type badges, and that type filter counts are consistent (Remote + Local = total).

---

## Preconditions

- User is logged in to the Elitea platform.
- Both Local MCPs (e.g., ADO, FileSystem, PlaywrightMCP) and Remote MCPs (e.g., Web Search, EliteaMCP, Github) exist in the project.

---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to MCP list page | MCP list page loads |
| 2 | Verify MCPs of both types coexist in the list (Local: ADO, FileSystem, PlaywrightMCP; Remote: Web Search, EliteaMCP, Github, etc.) | Both Local and Remote MCPs are visible |
| 3 | Verify each card shows correct type badge matching its actual type | Every card has a type badge matching its type |
| 6 | Apply "Remote" filter — count visible Remote MCPs | Remote MCP count is noted |
| 7 | Apply "Local" filter — count visible Local MCPs | Local MCP count is noted |
| 8 | Remove filter — verify total count = Remote count + Local count | Total MCPs equals the sum of Remote and Local counts |

---

## Expected Final State

The total MCP count equals the sum of Remote and Local counts when all filters are removed.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Type badges are correct; total count matches sum of filtered counts.

**Fail:**
- Any step produces an error or unexpected result.
- Type badges are incorrect, or total count does not match sum of Remote and Local.
