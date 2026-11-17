---
id: ELITEA-0831
title: "Run Details Dialog — Content and Real-Time Updates Across Sequential Runs"
priority: high
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [feat:pipelines, story:2186, epic:7093]
requirements: [ProjectAlita/projectalita.github.io#3584, ProjectAlita/projectalita.github.io#2186, EliteaAI/elitea_issues#7155, EliteaAI/elitea_issues#3734]
---
# ELITEA-0831: Run Details Dialog — Content and Real-Time Updates Across Sequential Runs

> **Updated for Pipelines 2.0:** UI wording only. Runs are triggered from the Test Pipeline panel (#7155), and the canvas "Run N details" chip is unchanged. The timeline groups nested agent/pipeline steps into one step (#3734).

> Retest pending

**Module:** Pipelines · **Priority:** High · **Type:** Functional

**Objective:** Verify the Run Details dialog (Timeline + States sections) is populated with current-run data at all times — not empty content or stale data from a prior run — across sequential runs in the same chat session.

**Coverage (parametrized):**

| Dimension | Values |
|---|---|
| Run number | 1st / 2nd / 3rd run in same chat session (no page refresh) |
| Open timing | While run is In Progress (mid-run) / After run completes |

## Preconditions

- A pipeline with at least one LLM node and at least one variable is saved.
- The pipeline is opened in the editor with the Test Pipeline panel open (or added as a participant in a Chat conversation).

## Test Data

- Pipeline: minimum 1 LLM node, 1 variable, saved
- Chat input to trigger a run: any text (e.g., "run")

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Trigger the 1st run (send a message in the Test Pipeline panel). | Pipeline starts. The "Run 1 details" chip appears on the canvas. |
| 2 | While the run is In Progress, click the run chip to open the Run Details dialog. | Dialog is NOT empty. Timeline section shows at least the run start timestamp and the first node in progress. Stop button is enabled. |
| 3 | Wait for the 1st run to complete. Observe the Run Details dialog. | Timeline shows all completed steps with timestamps (a nested agent/pipeline call appears as one step). States section shows before/after accordion entries for at least one pipeline variable. |
| 4 | Close the Run Details dialog. | Dialog closes. Flow view is visible. |
| 5 | Trigger a 2nd run. Immediately click the run chip to open Run Details. | Dialog reflects the new run's In-Progress state — Timeline shows the current run starting, NOT the 1st run's 'Completed' final state. Content is not empty. |
| 6 | Wait for the 2nd run to complete. Verify the dialog. | Timeline and States sections reflect the 2nd run's data. Data is not stale from the 1st run. |
| 7 | Repeat steps 5–6 for a 3rd run. | Run Details consistently reflects the active run after each trigger; no empty dialog and no data from previous runs. |

## Expected Final State

Run Details consistently reflects the active run after each trigger; no empty dialog and no data from previous runs.

## Pass/Fail Criteria

**Pass:**
- Run Details dialog is never empty when opened during or after a run
- Dialog always reflects the data of the currently active run
- No previous run data bleeds into the current run's dialog

**Fail:**
- Dialog appears empty on any run (including 2nd or 3rd)
- Dialog shows a prior run's final state immediately after a new run starts
- Timeline or States sections missing on any run
