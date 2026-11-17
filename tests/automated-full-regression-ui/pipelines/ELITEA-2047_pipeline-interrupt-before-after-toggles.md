---
id: ELITEA-2047
title: "Pipeline — Interrupt Before/After (Configured in YAML)"
priority: medium
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:pipelines, epic:7093]
requirements: [EliteaAI/elitea_issues#7157]
---

# ELITEA-2047: Pipeline — Interrupt Before/After (Configured in YAML)

> **Updated for Pipelines 2.0:** the per-node "Interrupt before/after" switches no longer exist in the node panel. Interrupts are now set through the pipeline-level `interrupt_before` / `interrupt_after` keys in the page Yaml. The checks themselves are unchanged: the run pauses at the interrupt point, the UI shows the paused state, and execution resumes and completes.

**Module:** pipelines · **Priority:** medium · **Type:** functional

**Objective:** Verify that `interrupt_before` and `interrupt_after` set in the pipeline YAML pause execution at the configured point, that the UI shows the paused state, and that execution resumes and completes.

---

## Preconditions

- User is logged in to the Elitea platform.
- A saved pipeline exists: "Code 1" (Code, entry point, returns a fixed value) → "Printer 1" (Printer, prints a fixed text) → End.

---

## Test Data

| Field | Value |
|-------|-------|
| Interrupt after (pipeline level) | `interrupt_after: [Code 1]` |
| Interrupt before (pipeline level) | `interrupt_before: [Printer 1]` |
| Run message | `go` |
| Resume message | `continue` |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the pipeline; switch the page toggle to "Yaml" | The page Yaml editor shows the pipeline definition; no `interrupt_before` / `interrupt_after` keys yet |
| 2 | Add the pipeline-level line `interrupt_after: [Code 1]`; click "Save" | Pipeline saves without errors |
| 3 | Switch to "Flow" | The edge "Code 1" → "Printer 1" shows the "Interrupt" label |
| 4 | Click "Test Pipeline"; send `go` | "Code 1" executes; execution pauses **after** "Code 1"; "Printer 1" has not run |
| 5 | Inspect the chat panel | The UI shows the paused state (e.g. "How to proceed? To resume the pipeline - type anything...") |
| 6 | Send `continue` | Execution resumes; "Printer 1" runs and its output appears; the run completes |
| 7 | In page "Yaml", replace the interrupt with `interrupt_before: [Printer 1]`; click "Save" | Pipeline saves without errors; `interrupt_after` is gone |
| 8 | Send `go` in the Test Pipeline panel | "Code 1" executes; execution pauses **before** "Printer 1"; "Printer 1" has not run |
| 9 | Inspect the chat panel | The UI shows the paused state |
| 10 | Send `continue` | Execution resumes; "Printer 1" runs and its output appears; the run completes |
| 11 | Reload the page; open page "Yaml" | `interrupt_before: [Printer 1]` is still present |

---

## Expected Final State

Both `interrupt_after` and `interrupt_before`, set in the pipeline YAML, pause execution at the configured point. The UI shows the paused state, the run resumes and completes after the user sends a message, and the setting persists after reload.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Execution pauses after "Code 1" with `interrupt_after`, and before "Printer 1" with `interrupt_before`; each run resumes and completes.

**Fail:**
- Execution does not pause at the configured point, the paused state is not shown, or the run cannot be resumed.
- The interrupt setting is lost after save and reload.
