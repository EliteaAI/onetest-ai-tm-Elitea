---
id: ELITEA-2008
title: "Entry Point Node — Trigger Restricted When HITL/Printer/Interrupts Present"
priority: medium
type: functional
module: pipelines
status: ready
execution_type: automated
automation_test_id:
  - tests.ui.pipelines.test_pipeline_entry_point_trigger_restricted_interactive_nodes.test_entry_point_trigger_restricted_interactive_nodes
automation_pr: https://github.com/EliteaAI/elitea-testing-public/commit/106d15f9
tags: [automated:UI:regression, feat:pipelines]
requirements: []
---

# ELITEA-2008: Entry Point Node — Trigger Restricted When HITL/Printer/Interrupts Present

**Module:** pipelines · **Priority:** medium · **Type:** functional

**Objective:** Verify that the Webhook trigger type is restricted (listed but disabled; only Chat Message is selectable) when a pipeline contains HITL nodes, Printer nodes, or static interrupt configurations, and that Chat Message and Webhook are both selectable again once those restrictions are removed.

---

## Preconditions

- User is logged in to the Elitea platform.
- A pipeline exists with an entry point node.

---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create a pipeline with any entry point node and a Printer node connected after it | Pipeline has entry point node + Printer node |
| 2 | Click the entry point node | Node configuration panel opens |
| 3 | Open Trigger dropdown | Trigger dropdown opens |
| 4 | Verify only "Chat Message" is selectable (Webhook is listed but disabled; Schedule is no longer a Trigger option, EL-7011) | "Chat Message" enabled, "Webhook" disabled |
| 5 | Remove Printer node, add HITL node instead — verify same restriction applies | With HITL node present, only "Chat Message" is selectable in Trigger dropdown |
| 6 | Remove HITL, add a non-entry-point node and set `interrupt_before: [<node id>]` in the YAML view (the per-node Interrupt before/after toggles were removed from node cards, EL-3872), Save — verify same restriction | With static interrupt enabled, only "Chat Message" is selectable |
| 7 | Remove all HITL/Printer/interrupt configurations — verify both trigger types become available again | Chat Message and Webhook are both enabled |

---

## Expected Final State

When Printer, HITL, or static interrupts are present in a pipeline, only the "Chat Message" trigger is selectable on the entry point node (Webhook disabled). Removing all such configurations re-enables both options.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Trigger dropdown correctly restricts to "Chat Message" (Webhook disabled) when incompatible nodes/interrupts are present, and restores all options when they are removed.

**Fail:**
- Any step produces an error or unexpected result.
- Webhook is selectable when it should be restricted, or do not reappear after restrictions are removed.
