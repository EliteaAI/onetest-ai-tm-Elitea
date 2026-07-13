---
id: ELITEA-1954
title: "MCP Integration in Pipeline — Change MCP Toolkit and Tool Selection"
priority: medium
type: functional
module: pipelines
status: draft
execution_type: automated
tags: [automated:UI:regression, feat:pipelines]
requirements: []
---

# ELITEA-1954: MCP Integration in Pipeline — Change MCP Toolkit and Tool Selection

**Module:** pipelines · **Priority:** medium · **Type:** functional

**Objective:** Verify that the Toolkit and Tool selections on an MCP node can be changed, that switching the Toolkit resets and repopulates the Tool dropdown, and that the new selections persist after saving.

---

## Preconditions

- User is logged in to the Elitea platform.
- A pipeline with an MCP node configured with a Toolkit and Tool is available.
- At least two MCPs are attached in the pipeline's TOOLS section.

---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open a pipeline with an MCP node already configured with a Toolkit and Tool | Configuration panel loads |
| 2 | Click on the MCP node to open configuration panel | Panel is visible |
| 3 | Note current Toolkit selection and Tool | Current selections are observed |
| 4 | Click "Toolkit" dropdown — verify it lists all MCPs attached in the pipeline's TOOLS section | All attached MCPs are listed |
| 5 | Select a different MCP | New Toolkit is selected |
| 6 | Verify "Tool" dropdown resets and repopulates with tools from the newly selected MCP | Tool dropdown shows tools from the new MCP |
| 7 | Select a tool from the new MCP | New tool is selected |
| 8 | Verify Input/Output variables update according to new tool | Variable chips reflect the new tool's parameters |
| 9 | Save pipeline | Pipeline is saved successfully |
| 10 | Reload — verify new Toolkit and Tool selections persisted | New selections are unchanged after reload |

---

## Expected Final State

The new Toolkit and Tool selections are persisted after saving and are confirmed on page reload.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Toolkit change resets Tool dropdown; new selections persist after save.

**Fail:**
- Any step produces an error or unexpected result.
- Tool dropdown does not reset on Toolkit change, or new selections are not persisted.
