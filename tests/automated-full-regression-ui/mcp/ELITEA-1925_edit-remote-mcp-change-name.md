---
id: ELITEA-1925
title: "Edit Remote MCP — Change Name"
priority: critical
type: functional
module: elitea-platform
status: draft
execution_type: manual
tags: [automated:UI:regression]
requirements: []
---

# ELITEA-1925: Edit Remote MCP — Change Name

**Module:** elitea-platform · **Priority:** medium · **Type:** functional

**Objective:** Verify that a Remote MCP's Toolkit Name can be edited, saved, and persisted correctly, and that the updated name is reflected in both the detail page header and the MCP list.

---

## Preconditions

- User is logged in to the Elitea platform.
- An existing Remote MCP named "Web Search" is available in the project.

---

## Test Data

| Field | Value |
|-------|-------|
| Original Name | Web Search |
| New Name | Web Search Renamed |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to MCPs list and open an existing Remote MCP (e.g., "Web Search") | Detail page loads with tab showing MCP name |
| 2 | Verify detail page loads with tab showing MCP name | Tab correctly shows "Web Search" |
| 3 | Click into "Toolkit Name *" field in Form view | Field becomes editable |
| 4 | Change name to "Web Search Renamed" | Field displays updated name |
| 5 | Verify Save button becomes enabled and Discard button becomes enabled | Both buttons are active |
| 6 | Click Save | Operation completes; confirmation or updated state is shown |
| 7 | Verify MCP name updates in the header | Header shows "Web Search Renamed" |
| 8 | Navigate to MCP list — verify updated name appears | List shows "Web Search Renamed" |
| 9 | Reopen MCP — verify name persisted | Detail page shows "Web Search Renamed" |
| 10 | Rename back to original "Web Search" and save | MCP name restored to "Web Search" |

---

## Expected Final State

The MCP name is successfully updated, persisted, and reflected in both the detail page and the MCP list; the name is reverted to "Web Search" after cleanup.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Name change is saved and visible in both the list and detail views.

**Fail:**
- Any step produces an error or unexpected result.
- Name change is not persisted after save.
