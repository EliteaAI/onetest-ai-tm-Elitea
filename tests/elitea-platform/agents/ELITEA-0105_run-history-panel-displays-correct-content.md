---
id: ELITEA-0105
title: "Run History panel displays correct content"
priority: high
type: functional
module: agents
status: ready
execution_type: manual
tags: [nfr:usability, eng:frontend, feat:agents, issue:3707, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3707]
---
# ELITEA-0105: Run History panel displays correct content

**Module:** Agents · **Priority:** High · **Type:** Functional

**Objective:** Verify that the Run History panel shows the correct table structure, past run entries, and allows loading a prior conversation.

**Coverage:**
- Panel title shows "Run History"
- Table columns: Date, Version, Duration
- Past run entries display correct date/time, version name, and duration
- Clicking a run entry loads that conversation into the chat area
- Close (X) button dismisses the panel

## Preconditions

- Logged in to {{base_url}} with a valid user account
- An Agent with at least 2–3 prior executions exists in the project

## Test Data

- Agent with known prior runs (e.g., runs from 16-03-2026 with versions `base`, `v3` and durations like `54.25s`, `4.51s`)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the Agents page. Open an agent that has prior executions. | Agent detail page opens. |
| 2 | Click the history/clock icon button in the top-right of the chat panel. | Run History panel opens. |
| 3 | Verify the panel title. | Title reads "Run History". |
| 4 | Verify the table columns. | Table has 3 columns: Date, Version, Duration (with sort arrows). |
| 5 | Verify each row contains a date/time value, a version name, and a duration in seconds. | All rows show valid data (e.g., `16-03-2026, 11:53 PM`, `base`, `54.25 s`). |
| 6 | Click on any row in the history table. | The corresponding conversation/run is loaded into the chat panel. |
| 7 | Click the X (Close) button on the Run History panel. | The panel closes. The chat area returns to its normal state. |

## Expected Final State

The panel closes. The chat area returns to its normal state.

## Pass/Fail Criteria

**Pass:**
- Panel title is "Run History"
- Table shows Date, Version, Duration columns with correct data
- Clicking a row loads the corresponding run into chat
- X button closes the panel without errors

**Fail:**
- Panel is blank or shows an error
- Columns are missing or show incorrect data
- Clicking a row does not load the conversation
- Panel cannot be closed
