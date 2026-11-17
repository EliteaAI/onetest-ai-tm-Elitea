---
id: ELITEA-4715
title: "Pipeline — View-Only Node Cards and Node Configuration Panel"
priority: high
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:pipelines, epic:7093]
requirements: [EliteaAI/elitea_issues#7157]
---

# ELITEA-4715: Pipeline — View-Only Node Cards and Node Configuration Panel

**Module:** pipelines · **Priority:** high · **Type:** functional

**Objective:** Verify that node cards on the canvas are view-only summaries, that clicking a card opens its configuration panel showing the same summarised data, that the entry point can be moved from the panel, and that the node Name field is validated and persisted.

---

## Preconditions

- User is logged in to the Elitea platform with Editor (or higher) role.
- A saved pipeline exists with three configured nodes: "Agent 1" (Agent, entry point) → "Toolkit 1" (Toolkit, with a toolkit and tool selected) → "Code 1" (Code) → End.

---

## Test Data

| Field | Value |
|-------|-------|
| New entry point | Code 1 |
| New node name | `Code renamed` |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the pipeline | Canvas shows the cards "Agent 1", "Toolkit 1", "Code 1" and "End" (`pipeline-node-card-<Name>`) |
| 2 | Inspect each node card | Each card shows only a header (type icon, node name, node type) and a summary area; no editable inputs, selects or text areas are present on the card |
| 3 | Inspect the entry-point badge | Only "Agent 1" shows the "Entrypoint" badge |
| 4 | Read the summary text on the "Toolkit 1" card (`pipeline-node-summary-primary`); click the card | The node configuration panel opens on the right. The toolkit/tool name shown on the card is also shown in the panel's Basic section (`pipeline-node-panel-basic-section`) (partial text match) |
| 5 | Click the "Agent 1" card | The panel switches to "Agent 1"; the agent name shown on the card is shown in the panel (partial text match) |
| 6 | Click the panel's "✕" close button | The panel closes; the canvas is shown without the panel |
| 7 | Click the "Code 1" card; click "Make Entrypoint" in the panel footer | "Code 1" now shows the "Entrypoint" badge; "Agent 1" no longer shows it |
| 8 | In the "Code 1" panel, clear the "Name" field | Validation message "Name is required" is shown; "Save" is disabled |
| 9 | Enter `Code renamed` in the "Name" field | The validation message disappears; the card title on the canvas updates to "Code renamed" |
| 10 | Click "Save"; reload the page | The pipeline reloads; the card "Code renamed" is present and has the "Entrypoint" badge |

---

## Expected Final State

Cards are view-only summaries; the panel is the only place to edit a node; the entry point moved to "Code renamed" and the rename persisted after reload.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- No editable field exists on any card; panel open/switch/close works; Make Entrypoint, Name validation and rename persist after reload.

**Fail:**
- Any card contains an editable control.
- The panel shows data inconsistent with the card summary.
- Empty Name is accepted, or the rename / new entry point is lost after reload.

**Notes:** Per-node-type required fields are covered by the node-configuration cases (ELITEA-2004, 2009, 2010, 2014, 2033, 2034, 2035, 2037, 2038, 2039) and are not repeated here.
