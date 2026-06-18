---
id: ELITEA-0831
title: "Run Details Dialog — Content and Real-Time Updates Across Sequential Runs"
priority: high
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [feat:pipelines, story:2186]
requirements: [ProjectAlita/projectalita.github.io#3584, ProjectAlita/projectalita.github.io#2186]
---
# ELITEA-0831: Run Details Dialog — Content and Real-Time Updates Across Sequential Runs

**Module:** Pipelines · **Priority:** High · **Type:** Functional

**Objective:** Verify the Run Details dialog (Timeline + States sections) is populated with current-run data at all times — not empty content or stale data from a prior run — across sequential runs in the same chat session.

**Coverage (parametrized):**

| Dimension | Values |
|---|---|
| Run number | 1st / 2nd / 3rd run in same chat session (no page refresh) |
| Open timing | While run is In Progress (mid-run) / After run completes |

## Preconditions

- A pipeline with at least one LLM node and at least one variable is published.
- The pipeline is added as a participant in a Chat conversation.

## Test Data

- Pipeline: minimum 1 LLM node, 1 variable, published
- Chat input to trigger a run: any text (e.g., "run")

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | In chat with the pipeline participant, trigger the 1st run. | Pipeline starts. Run chipset appears in Flow View. |
| 2 | While the run is In Progress, click the run chipset to open the Run Details dialog. | Dialog is NOT empty. Timeline section shows at least the run start timestamp and the first node in progress. Stop button is enabled. |
| 3 | Wait for the 1st run to complete. Observe the Run Details dialog. | Timeline shows all completed steps with timestamps. States section shows before/after accordion entries for at least one pipeline variable. |
| 4 | Close the Run Details dialog. | Dialog closes. Flow View is visible. |
| 5 | Trigger a 2nd run. Immediately click the chipset to open Run Details. | Dialog reflects the new run's In-Progress state — Timeline shows the current run starting, NOT the 1st run's 'Completed' final state. Content is not empty. |
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
