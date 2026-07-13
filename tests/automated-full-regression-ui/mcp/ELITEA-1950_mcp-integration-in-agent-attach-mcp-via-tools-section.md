---
id: ELITEA-1950
title: "MCP Integration in Agent — Attach MCP via Tools Section"
priority: medium
type: functional
module: agents
status: draft
execution_type: automated
tags: [automated:UI:regression, feat:agents]
requirements: []
---

# ELITEA-1950: MCP Integration in Agent — Attach MCP via Tools Section

**Module:** agents · **Priority:** medium · **Type:** functional

**Objective:** Verify that a Remote MCP can be attached to an agent via the MCP tab in the Tools section, persists after saving, and can be removed successfully.

---

## Preconditions

- User is logged in to the Elitea platform.
- An existing agent is available in the project.
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
| 1 | Navigate to Agents section and open any agent's detail page | Agent detail page loads |
| 2 | Scroll to "Tools" section — verify it is expanded | Tools section is visible and expanded |
| 3 | Verify tool type tabs are visible: Toolkit, MCP, Agent, Pipeline | All four tabs are shown |
| 4 | Click "MCP" tab button | MCP tab is active |
| 5 | Verify MCP selection area appears (dropdown or list to select from project MCPs) | MCP selection UI is displayed |
| 6 | Select a Remote MCP from the dropdown (e.g., "Web Search") | MCP is selected |
| 7 | Verify selected MCP appears in the tools list under MCP tab | "Web Search" appears in the tools list |
| 8 | Click Save on agent | Operation completes successfully |
| 9 | Reload page — verify MCP is still attached under MCP tab | MCP persists after reload |
| 10 | Remove the MCP attachment — save and verify it's gone | MCP is no longer listed under MCP tab |

---

## Expected Final State

The MCP attachment is removed from the agent's tools list after saving.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- MCP is attached, persists after reload, and can be removed.

**Fail:**
- Any step produces an error or unexpected result.
- MCP is not attached, not persisted, or cannot be removed.
