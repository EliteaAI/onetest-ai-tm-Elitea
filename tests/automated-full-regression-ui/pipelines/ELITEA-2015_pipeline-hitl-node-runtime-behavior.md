---
id: ELITEA-2015
title: "Pipeline HITL Node — Runtime Behavior"
priority: high
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:pipelines, epic:7093]
requirements: [EliteaAI/elitea_issues#7157]
---

# ELITEA-2015: Pipeline HITL Node — Runtime Behavior

> **Updated for Pipelines 2.0:** rewritten with concrete topology, configuration via the node panel, exact messages, and two runs (Approve, then Reject).

**Module:** pipelines · **Priority:** high · **Type:** functional

**Objective:** Verify that during pipeline execution a HITL node pauses execution and shows Approve / Edit / Reject actions, and that Approve and Reject route the flow to their configured targets.

---

## Preconditions

- User is logged in to the Elitea platform.
- An LLM model is available in the project.

---

## Test Data

| Field | Value |
|-------|-------|
| Topology | "LLM 1" (LLM, entry point) → "HITL 1" (HITL) → "Printer 1" (Printer) → End |
| LLM 1 Task | `Write one sentence about testing` |
| HITL 1 USER MESSAGE | Fixed: `Please review the generated sentence` |
| HITL 1 routes | Approve → Printer 1 · Edit → Printer 1 · Reject → End |
| Printer 1 text | Fixed: `Approved output printed` |
| Run message | `start` |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create a pipeline; add the nodes and configure them in the node panels per Test Data; click "Save" | Pipeline saves; canvas shows LLM 1 → HITL 1 → Printer 1 → End, with HITL routes drawn to "Printer 1" and "End" |
| 2 | Click "Test Pipeline"; send `start` | "LLM 1" runs and its response appears |
| 3 | Wait for the run to reach "HITL 1" | Execution pauses. The panel shows the message "Please review the generated sentence" and the buttons "Approve", "Edit", "Reject". "HITL 1" is highlighted on the canvas |
| 4 | Click "Approve" | Flow continues to "Printer 1"; the text "Approved output printed" appears in the panel; the run completes |
| 5 | Send `start` again; wait for the HITL pause | The HITL message and the "Approve" / "Edit" / "Reject" buttons appear again |
| 6 | Click "Reject" | The flow goes to End; "Approved output printed" does NOT appear for this run; the run completes |

---

## Expected Final State

The HITL node pauses execution and offers Approve / Edit / Reject; Approve routes to "Printer 1" (printed output shown); Reject ends the pipeline without the Printer output.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The HITL pause shows the configured message and all three buttons.
- Approve and Reject route to their configured targets.

**Fail:**
- HITL does not pause, buttons are missing, or routing does not match the configuration.
