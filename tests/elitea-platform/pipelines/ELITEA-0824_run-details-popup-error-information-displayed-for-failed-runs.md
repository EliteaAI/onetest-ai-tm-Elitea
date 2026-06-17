---
id: ELITEA-0824
title: "Run Details Popup — Error Information Displayed for Failed Runs"
priority: high
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [feat:pipelines, story:2186]
requirements: [ProjectAlita/projectalita.github.io#2186]
---
# ELITEA-0824: Run Details Popup — Error Information Displayed for Failed Runs

**Module:** Pipelines · **Priority:** High · **Type:** Functional

**Objective:** Verify the Run Details popup correctly displays error information — including error message, status indicator, and failure timestamp — when opened for a run that failed during execution.

**Coverage:**
- Popup opens for error-state (red info icon) runs
- Red info icon displayed in popup header
- Status label indicates "Error" or "Failed"
- Error details section present with error message/description
- Failure timestamp present
- Input data still shown; output section indicates no output generated

## Preconditions

- Logged in at {URL}, project {Project} selected
- Pipeline "Test Pipeline — Error Popup" created: LLM node with Task field empty (triggers execution error), set as entrypoint, saved
- Pipeline open on Configuration tab → Flow View

## Test Data

- Pipeline name: "Test Pipeline — Error Popup"
- LLM node Task field: empty string (triggers error)
- Chat input: "run"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Type "run" in chat input. Press Enter. Wait for run to fail. | Run chipset transitions from blue loading to red info icon. Run 1 is in error state. |
| 2 | Click the Run 1 chipset to open the popup. | Run Details popup opens. |
| 3 | Verify popup header: shows "Run 1", red info icon, status label is "Error" or "Failed". | Error state clearly indicated with correct icon and label. |
| 4 | Verify an error details section is present containing at least an error message or description. | Human-readable error information visible in the popup. |
| 5 | Verify a failure timestamp is present. | Timestamp showing when the error occurred is displayed. |
| 6 | Verify output section indicates no output was produced. | Output section is empty or shows "No output" / equivalent message. |
| 7 | Close the popup. | Popup closes cleanly. Flow View restored. |

## Expected Final State

Popup closes cleanly. Flow View restored.

## Pass/Fail Criteria

**Pass:**
- Popup opens for error-state run
- Red icon and "Error"/"Failed" label visible in popup
- Error details section contains a meaningful message
- Failure timestamp present
- No output shown for failed run
- Popup closes normally

**Fail:**
- Popup does not open for error runs
- Error section absent or empty
- Popup shows wrong status (e.g., green checkmark)
- No timestamp shown
- Popup crashes or shows an unhandled exception
