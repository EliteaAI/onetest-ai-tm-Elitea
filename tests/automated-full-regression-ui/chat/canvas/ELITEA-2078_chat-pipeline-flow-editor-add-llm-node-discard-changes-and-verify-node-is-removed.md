---
id: ELITEA-2078
title: "Chat – Pipeline Flow Editor – Add LLM Node, Discard Changes, and Verify Node is Removed"
priority: medium
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2078: Chat – Pipeline Flow Editor – Add LLM Node, Discard Changes, and Verify Node is Removed

**Module:** chat-interface · **Priority:** medium · **Type:** functional

**Objective:** Verify that adding an LLM node to the Flow Editor and then clicking Discard removes the unsaved node and reverts the canvas to its last saved state.

---

## Preconditions

- User is logged in to the Elitea platform.
- The "test-pipeline" canvas is open with "Configuration" and "Flow Editor" tabs (following ELITEA-2077).

---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Verify the "test-pipeline" canvas is open with "Configuration" and "Flow Editor" tabs | Canvas is in edit mode |
| 2 | Click on the "Flow Editor" tab | Flow Editor opens with grid canvas background |
| 3 | Verify "Flow" and "Yaml" sub-tabs appear; "Flow" tab is active; only "End" node is visible | Flow editor initialized correctly |
| 4 | Click the "+ Add node" button in the top right | Node type selector menu opens |
| 5 | Verify the menu shows node types including: Agent, MCP, Code, Printer, Custom, Router, Decision, State modifier, Human-in-the-loop, Toolkit, LLM | All node types listed |
| 6 | Click on "LLM" from the menu | LLM node is added to the canvas |
| 7 | Verify the LLM node appears with icon, label, and connection ports | LLM node is visible and selectable |
| 8 | Click the "Discard" button without saving | Confirmation dialog appears |
| 9 | Click "Discard" or "Yes" to confirm | Canvas updates; LLM node is removed |
| 10 | Verify only the "End" node remains on the canvas | Canvas reverted to last saved state |

---

## Expected Final State

The LLM node is removed after discarding; only the "End" node remains, matching the last saved state of the flow.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- LLM node is removed after discarding; only the End node remains.

**Fail:**
- Any step produces an error or unexpected result.
- LLM node persists after discarding, or the canvas does not revert.
