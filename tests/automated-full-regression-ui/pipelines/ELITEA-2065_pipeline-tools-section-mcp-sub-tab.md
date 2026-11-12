---
id: ELITEA-2065
title: "Pipeline — Tools Section — MCP Sub-tab with Tool Selection"
priority: medium
type: functional
module: pipelines
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:pipelines]
requirements: []
automation_test_id:
  - tests.ui.pipelines_2.test_pipeline_tools_section_mcp_add_view_remove.test_tools_section_mcp_add_view_remove
automation_pr: https://github.com/EliteaAI/elitea-testing-public/commit/10d28ba6
---

# ELITEA-2065: Pipeline — Tools Section — MCP Sub-tab with Tool Selection

**Module:** pipelines · **Priority:** medium · **Type:** functional

**Objective:** Verify that an MCP can be added to a pipeline's Tools section by selecting it in an MCP node's picker, and detached by clearing it from the node, and that the removal persists after save.

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
| 1 | Open a pipeline | Pipeline is loaded in the editor |
| 2 | Add an MCP node via the canvas and open its picker (search box, "Create new", project-wide list) | The picker lists the project's MCPs, including "WebSearch" |
| 3 | Select an MCP in the node's picker (e.g., "WebSearch") | MCP is selected on the node |
| 4 | Verify the MCP was auto-attached to the left TOOLS section (no "+ MCP" button click) | "WebSearch" appears as a card in TOOLS |
| 5 | Verify MCP shows its name and tools count or list | MCP entry displays name and tool information |
| 6 | Click on the attached MCP entry to see its tools/details | MCP details or tools list is shown |
| 7 | Open the MCP node's config panel and click the clear (X) button next to the MCP selection (BASIC section) | MCP selection is cleared from the node |
| 8 | Verify the MCP card disappears from the TOOLS section | "WebSearch" no longer appears in TOOLS (no node uses it, so it auto-detaches) |
| 9 | Save and reload — verify removal persists | MCP is absent from TOOLS after save and reload |

---

## Expected Final State

An MCP can be added to the Tools section MCP sub-tab, its details viewed, and removed. The removal persists after saving.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- MCP is added to Tools, details are viewable, and removal persists after save.

**Fail:**
- Any step produces an error or unexpected result.
- MCP cannot be added, details are not shown, or removal is not saved.
