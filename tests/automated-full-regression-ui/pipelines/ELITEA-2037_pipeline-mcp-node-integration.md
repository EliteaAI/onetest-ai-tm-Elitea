---
id: ELITEA-2037
title: "Pipeline — MCP Node Integration"
priority: high
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:pipelines]
requirements: []
---

# ELITEA-2037: Pipeline — MCP Node Integration

**Module:** pipelines · **Priority:** high · **Type:** functional

**Objective:** Verify that an MCP can be attached to a pipeline, an MCP node added and configured with tool-specific INPUT MAPPING, and that all configuration persists after save and reload.

---

## Preconditions

- User is logged in to the Elitea platform.
- An existing MCP (e.g., "WebSearch") is available in the project.

---

## Test Data

| Field | Value |
|-------|-------|
| MCP name | WebSearch |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open a pipeline (or create new one) | Pipeline is open and ready for editing |
| 2 | In the left panel "Tools" section, click "+ MCP" button | MCP picker popup opens |
| 3 | From the MCP picker popup, select an existing MCP (e.g., "WebSearch") | MCP is selected |
| 4 | Verify MCP appears in Tools list under MCP sub-tab | "WebSearch" is listed under the MCP sub-tab in Tools |
| 5 | Click "Add node" on canvas → select "MCP" | MCP node is added to the canvas |
| 6 | Verify MCP node panel shows: Toolkit dropdown, Tool dropdown, Input, Output, INPUT MAPPING (REQUIRED N), INPUT MAPPING (OPTIONAL N), Interrupt before/after, Structured output | All listed sections are present |
| 7 | Select attached MCP from "Toolkit" dropdown | MCP is selected in the Toolkit dropdown |
| 8 | Select a tool from "Tool" dropdown — verify INPUT MAPPING sections populate with tool-specific parameters | INPUT MAPPING sections appear with tool parameters |
| 9 | Configure required INPUT MAPPING fields (Type + Value for each) | INPUT MAPPING values are set |
| 10 | Set Input/Output comboboxes | Input and Output variables are configured |
| 11 | Save pipeline | Pipeline saves without errors |
| 12 | Reload — verify Toolkit, Tool, and INPUT MAPPING values persist | All MCP node configuration persists after reload |

---

## Expected Final State

The MCP node is fully configured with Toolkit, Tool, INPUT MAPPING, Input, and Output, all persisting after save and reload. The MCP appears in the Tools section under the MCP sub-tab.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- MCP node configuration including Toolkit, Tool, and INPUT MAPPING persists after reload.

**Fail:**
- Any step produces an error or unexpected result.
- Any MCP node configuration field is lost after saving.
