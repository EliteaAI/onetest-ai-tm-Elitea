---
id: ELITEA-1953
title: "MCP Integration in Pipeline — MCP Node Input Mapping Configuration"
priority: high
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:pipelines]
requirements: []
---

# ELITEA-1953: MCP Integration in Pipeline — MCP Node Input Mapping Configuration

**Module:** pipelines · **Priority:** high · **Type:** functional

**Objective:** Verify that the INPUT MAPPING section of an MCP node in a pipeline lists all tool parameters with their types, supports type configuration, and that all settings including interrupt and structured output toggles persist after saving.

---

## Preconditions

- User is logged in to the Elitea platform.
- A pipeline with an MCP node is available, with a Toolkit and Tool already selected.

---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open a pipeline containing an MCP node that has a Toolkit | Configuration panel is visible |
| 2 | Select a tool from "Tool" dropdown (e.g., "get_auth_user") | Tool is selected |
| 3 | Verify "INPUT MAPPING (REQUIRED)" section is shown at bottom of panel | Input mapping section is visible |
| 4 | Verify all input parameters of the selected MCP tool are listed with their names and types | All parameters are listed with correct names and types |
| 7 | Change Type from "Fixed" to another option if available (e.g., "Variable") | Type selector updates |
| 8 | Configure input mapping value | Input mapping value is set |
| 9 | Verify "Interrupt before" and "Interrupt after" toggles are present (disabled by default) | Both interrupt toggles are visible and disabled |
| 10 | Verify "Structured output" toggle is present (disabled by default) | Structured output toggle is visible and disabled |
| 11 | Save pipeline | Pipeline is saved successfully |
| 12 | Reload — verify input mapping configuration persisted | Input mapping settings are unchanged after reload |

---

## Expected Final State

All input mapping configuration including type, value, and toggles are persisted correctly after saving and reloading.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Input mapping settings persist after save and reload.

**Fail:**
- Any step produces an error or unexpected result.
- Input mapping parameters are missing or settings do not persist after reload.
