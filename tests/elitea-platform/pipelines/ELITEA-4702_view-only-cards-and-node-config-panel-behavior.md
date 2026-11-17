---
id: ELITEA-4702
title: "View-only Node Cards and Node Configuration Panel — Open, Close and General Behavior"
priority: high
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [feat:pipelines, epic:7093, r-2.0.8]
requirements: [EliteaAI/elitea_issues#7157]
---
# ELITEA-4702: View-only Node Cards and Node Configuration Panel — Open, Close and General Behavior

**Module:** Pipelines · **Priority:** High · **Type:** Functional

**Objective:** Verify that node cards are view-only summaries (no inline controls), that canvas interactions still work on them, and that the right-side node configuration panel opens, switches, closes and applies edits immediately as specified.

**Coverage:**
- Card: header + summary only; no ⋮ menu, no collapse toggle, no Trigger on the card
- "Not configured" summary and red status icon; summary updates live once configured
- Drag, connect, create from card still work; Del/Backspace delete
- Panel: open on click (no pan/zoom), switch, close via ✕ / Esc / empty canvas
- Panel header, Flow/YAML toggle, Name → Basic (expanded) → Advanced (collapsed), scrollable content
- Edits apply live; page-level Save persists; no in-panel Save/Cancel
- Footer: Make Entrypoint (toast), Delete (confirmation)
- Panel open together with the Test panel
- See ELITEA-4715 for the main flow

## Preconditions

- Logged in to {{base_url}}
- A saved pipeline with Agent (entry point), LLM and Code nodes; at least one agent exists in the project

## Test Data

- New name for Code node: `Code renamed`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Observe any card. | Only header (icon, name, type, Entrypoint badge if entry) + summary. No editable fields, no ⋮ menu, no collapse button, no Trigger selector. |
| 2 | Add a new Agent node; do not configure it. | Card summary reads **Not configured**; red status icon on the card with tooltip *"Select an agent"*. |
| 3 | Open its panel and select an agent; set Task. | The card summary updates immediately to the selected agent name and task preview — no refresh needed. |
| 4 | Drag a card; connect two cards; create a node from a card's Output. | All three interactions work on the view-only cards. Dragging does **not** open the panel. |
| 5 | Single-click a card. | The card is selected and the panel opens on the right; the canvas does not pan or zoom. |
| 6 | Observe the panel header. | Node type icon, type name, type description (same text as in the node-type list), ✕. Flow/YAML toggle with Flow selected. |
| 7 | Observe the panel content. | **Name\*** first, then **Basic** (expanded), then **Advanced** (collapsed). The content between header and footer scrolls independently. |
| 8 | Click another card. | The panel switches to that node; no stale content. |
| 9 | Close the panel with ✕; reopen; close with **Esc**; reopen; click empty canvas. | Each closes the panel and clears selection. |
| 10 | Edit a field in the panel. | The YAML, the card summary and Save update immediately. There is no Save/Cancel inside the panel; page-level Save persists. |
| 11 | Clear the Name field. | Inline error, Save disabled. |
| 12 | Set Name to an existing node's name. | Inline error *"The name has been used by other nodes, please input a new name!"*. |
| 13 | Set Name to `Code renamed`. | Card title updates. |
| 14 | On a non-entry node, click **Make Entrypoint**. | Toast *"[node name] is set as entrypoint"*; button becomes the non-clickable **Entrypoint** state; Entrypoint badge moves to that card. |
| 15 | Click the footer **Delete** icon; click **Cancel**; click it again and **Delete**. | Dialog *"Are you sure to delete the <name> node? It can't be restored."*. Cancel keeps the node; Delete removes node + card and closes the panel. |
| 16 | Select a card and press **Del** / **Backspace**. | The same delete confirmation dialog appears. |
| 17 | Open the Test panel while a node panel is open. | Both panels are open together; neither replaces the other. |
| 18 | Open a field that has an AI Assistant (e.g. Code, Printer, LLM System/Task) and use it. | AI Assistant is present in the panel and changes the field value as today. |

## Expected Final State

Cards are view-only summaries; all editing happens in the right-side panel, which opens/switches/closes correctly, applies edits live and persists via page-level Save.

## Pass/Fail Criteria

**Pass:**
- No inline controls on cards; Not configured / live summary update work
- Canvas interactions and keyboard delete still work
- Panel open/switch/close behaviors as described
- Name validation, Make Entrypoint toast, Delete confirmation as described

**Fail:**
- Any editable control on a card
- Panel opens on drag, pans/zooms the canvas, or shows stale content
- Edits not applied live, or an in-panel Save is required
