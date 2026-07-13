---
id: ELITEA-1955
title: "MCP Integration in Pipeline — MCP Node Without Tool Attached First"
priority: medium
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:pipelines]
requirements: []
---

# ELITEA-1955: MCP Integration in Pipeline — MCP Node Without Tool Attached First

**Module:** pipelines · **Priority:** medium · **Type:** functional

**Objective:** Verify that an MCP node added before attaching an MCP tool shows an empty Toolkit dropdown, and that after attaching an MCP the toolkit becomes available and the node can be configured and saved.

---

## Preconditions

- User is logged in to the Elitea platform.
- A Remote MCP (e.g., "Web Search") is available in the project.

---

## Test Data

| Field | Value |
|-------|-------|
| MCP to attach | Web Search |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create a new pipeline | Pipeline canvas loads |
| 2 | Do NOT attach any MCP in the TOOLS section | TOOLS section has no MCP |
| 3 | Click "Add node" and select "MCP" | MCP node is added to the canvas |
| 4 | Click on the MCP node to open configuration | Configuration panel opens |
| 5 | Click "Toolkit" dropdown | Dropdown opens |
| 6 | Verify dropdown is empty or shows message indicating no MCP tools are attached | Dropdown is empty or shows appropriate message |
| 7 | Go back to left panel TOOLS section and click "+ MCP" | MCP selection appears |
| 8 | Attach a Remote MCP (e.g., "Web Search") | MCP is attached in TOOLS section |
| 9 | Click on MCP node again — open "Toolkit" dropdown | Dropdown opens |
| 10 | Verify newly attached MCP now appears in the dropdown | "Web Search" is listed in the dropdown |
| 11 | Select it and configure a tool | Tool is selected |
| 12 | Save pipeline — verify configuration persists | Pipeline is saved and configuration is correct |

---

## Expected Final State

The MCP node is configured with a Toolkit and Tool, and the pipeline is saved successfully.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Toolkit dropdown is empty before attachment and populates after; configuration persists.

**Fail:**
- Any step produces an error or unexpected result.
- Toolkit dropdown does not populate after MCP attachment, or configuration does not persist.
