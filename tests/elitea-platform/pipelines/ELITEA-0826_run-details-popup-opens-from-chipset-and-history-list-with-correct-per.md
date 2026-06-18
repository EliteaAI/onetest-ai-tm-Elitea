---
id: ELITEA-0826
title: "Run Details Popup — Opens from Chipset and History List with Correct Per-Run Data"
priority: high
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [feat:pipelines, story:2186]
requirements: [ProjectAlita/projectalita.github.io#2186]
---
# ELITEA-0826: Run Details Popup — Opens from Chipset and History List with Correct Per-Run Data

**Module:** Pipelines · **Priority:** High · **Type:** Functional

**Objective:** Verify the Run Details popup opens when clicking both the current run chipset and runs in the History list, and that the content displayed matches the specific selected run (correct input, output, timestamps, and run number).

**Coverage:**
- Popup accessible from current run chipset (click on chipset)
- Popup accessible from History Icon list entries
- Popup displays run number, status icon, timestamps, input data, output data
- Data is run-specific — each popup shows its own run's data, not another run's
- Close mechanism works (X button or click-outside)

## Preconditions

- Logged in at {URL}, project {Project} selected
- Pipeline "Test Pipeline — Run Details Popup" created: LLM node (System: "You must create story", Task: "Create some interesting long story"), set as entrypoint, saved
- Pipeline open on Configuration tab → Flow View
- Three completed runs already executed with distinct chat inputs before starting steps

## Test Data

- Pipeline name: "Test Pipeline — Run Details Popup"
- Run 1 chat input: "First run data"
- Run 2 chat input: "Second run data"
- Run 3 chat input: "Third run data"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Verify Run 3 is the current run with green checkmark. History Icon visible. | Run 3 chipset and History Icon present. |
| 2 | Click the Run 3 chipset. | Run Details popup opens. |
| 3 | Verify popup content: shows "Run 3", green checkmark status, timestamps present, input shows "Third run data", output section populated. | All sections present and contain Run 3's data. |
| 4 | Close the popup via the X button or close action. | Popup closes. Flow View visible. |
| 5 | Click the History Icon. Click Run 1 in the list. | Run Details popup opens for Run 1. |
| 6 | Verify popup content: shows "Run 1", green checkmark, input shows "First run data", output is Run 1's output. | Content is Run 1's data — not Run 2 or Run 3's data. |
| 7 | Close popup. Click History Icon. Click Run 2 in the list. | Run Details popup opens for Run 2. |
| 8 | Verify popup shows "Run 2", input shows "Second run data". Data differs from Run 1 and Run 3. | Each popup is run-specific with no cross-contamination. |
| 9 | Close popup. | Popup closes cleanly. Flow View restored. |

## Expected Final State

Popup closes cleanly. Flow View restored.

## Pass/Fail Criteria

**Pass:**
- Popup opens from both current chipset and history list entries
- Each popup shows data exclusive to the selected run
- All sections (status, timestamp, input, output) populated
- Close mechanism works from all entry points

**Fail:**
- Popup does not open on click
- Popup shows data from the wrong run
- Any required section (input/output/timestamp) is empty or missing
- Popup cannot be closed
