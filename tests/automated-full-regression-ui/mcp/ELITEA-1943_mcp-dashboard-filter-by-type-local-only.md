---
id: ELITEA-1943
title: "MCP Dashboard — Filter by Type (Local only)"
priority: high
type: functional
module: elitea-platform
status: draft
execution_type: manual
tags: [automated:UI:regression]
requirements: []
---

# ELITEA-1943: MCP Dashboard — Filter by Type (Local only)

**Module:** elitea-platform · **Priority:** medium · **Type:** functional

**Objective:** Verify that the "Local" type filter on the MCP list page shows only Local MCPs and hides Remote MCPs, and that removing the filter restores all MCPs.

---

## Preconditions

- User is logged in to the Elitea platform.
- Both Local MCPs (e.g., ADO, FileSystem, PlaywrightMCP) and Remote MCPs exist in the project.

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
| 2 | Click "Local" filter button | Local filter is applied |
| 3 | Verify only MCPs with "Local" type badge are displayed (e.g., "ADO", "FileSystem", "PlaywrightMCP") | Only Local MCPs are shown |
| 4 | Verify Remote MCPs are hidden | Remote MCPs are not visible |
| 5 | Remove filter — verify all MCPs return | All MCPs are visible again |

---

## Expected Final State

All MCPs return to the list after the Local filter is removed.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Local filter correctly hides Remote MCPs and restores all on removal.

**Fail:**
- Any step produces an error or unexpected result.
- Filter does not hide Remote MCPs or all MCPs do not return after removal.
