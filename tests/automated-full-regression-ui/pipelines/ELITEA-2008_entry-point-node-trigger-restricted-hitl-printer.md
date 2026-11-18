---
id: ELITEA-2008
title: "Pipeline Schedule — Blocked When HITL/Printer/Interrupts Present"
priority: medium
type: functional
module: pipelines
status: ready
execution_type: automated
automation_test_id:
  - tests.ui.pipelines.test_pipeline_entry_point_trigger_restricted_interactive_nodes.test_entry_point_trigger_restricted_interactive_nodes
automation_pr: https://github.com/EliteaAI/elitea-testing-public/commit/1e43c0d2
tags: [automated:UI:regression, feat:pipelines]
requirements: []
---

# ELITEA-2008: Pipeline Schedule — Blocked When HITL/Printer/Interrupts Present

**Module:** pipelines · **Priority:** medium · **Type:** functional

**Objective:** Verify that the New Schedule page (SCHEDULES section → "+ Schedule") blocks saving a schedule for a pipeline containing a Printer node, a HITL node, or a static interrupt, and that the block disappears once they are removed. (Schedule moved out of the Trigger dropdown — EliteaAI/elitea_issues#7011, #7338. The old Webhook-disabled checks are under review: see elitea-testing-public#2985.)

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
| 1 | Pipeline with an entry point node and a Printer node after it → SCHEDULES → "+ Schedule" | Risk message shown ("This pipeline asks a person for input at step '<node>'…", "Scheduled runs can't answer it.", "You can't save this schedule.", "Remove the human-input step, or run the pipeline from the chat." + link "Open pipeline to change steps"); Save disabled with "Fix the risk check to save" next to it |
| 2 | Click "Open pipeline to change steps"; replace the Printer with a HITL node; Save; SCHEDULES → "+ Schedule" | Same risk message; Save disabled |
| 3 | Replace the HITL with a plain node and set `interrupt_before: [<node id>]` in the page Yaml; Save; SCHEDULES → "+ Schedule" | Same risk message; Save disabled |
| 4 | Remove the interrupt (no Printer / HITL / interrupt left); Save; SCHEDULES → "+ Schedule" | No risk message; Save is enabled |

---|--------|-----------------|
| 1 | Create a pipeline with any entry point node and a Printer node connected after it | Pipeline has entry point node + Printer node |
| 2 | Click the entry point node | Node configuration panel opens |
| 3 | Open Trigger dropdown | Trigger dropdown opens |
| 4 | Verify only "Chat Message" is selectable (Webhook is listed but disabled; Schedule is no longer a Trigger option, EL-7011) | "Chat Message" enabled, "Webhook" disabled |
| 5 | Remove Printer node, add HITL node instead — verify same restriction applies | With HITL node present, only "Chat Message" is selectable in Trigger dropdown |
| 6 | Remove HITL, add a non-entry-point node and set `interrupt_before: [<node id>]` in the YAML view (the per-node Interrupt before/after toggles were removed from node cards, EL-3872), Save — verify same restriction | With static interrupt enabled, only "Chat Message" is selectable |
| 7 | Remove all HITL/Printer/interrupt configurations — verify both trigger types become available again | Chat Message and Webhook are both enabled |

---

## Expected Final State

When Printer, HITL, or static interrupts are present, the New Schedule page shows the risk message and Save is disabled. Removing all of them clears the message and enables Save.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Risk message + disabled Save for Printer, HITL and interrupt; no message and enabled Save once removed.

**Fail:**
- Any step produces an error or unexpected result.
- Save is enabled when it should be blocked, or the block remains after the restrictions are removed.
