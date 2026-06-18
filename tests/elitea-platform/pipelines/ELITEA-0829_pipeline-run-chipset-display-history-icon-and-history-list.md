---
id: ELITEA-0829
title: "Pipeline Run Chipset — Display, History Icon, and History List"
priority: critical
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [feat:pipelines, story:2186]
requirements: [ProjectAlita/projectalita.github.io#2186]
---
# ELITEA-0829: Pipeline Run Chipset — Display, History Icon, and History List

**Module:** Pipelines · **Priority:** Critical · **Type:** Functional

**Objective:** Verify the redesigned run chipset renders with a status icon and run number, that the History Icon appears in Flow View only when 2+ runs exist, and that the history list shows all previous runs except the current one.

**Coverage:**
- Chipset shows status icon + "Run N" label on first execution
- No History Icon visible with 0 or 1 runs
- History Icon appears immediately when 2nd run completes
- Current (most recent) run is displayed separately, not grouped into history
- History list shows all completed previous runs with their status icons
- Current run excluded from history list
- All runs executed via chat input in Configuration tab (Flow View)

## Preconditions

- Logged in at {URL} with {Username} / {Password}, project {Project} selected
- Pipeline "Test Pipeline — Chipset and History" created: LLM node (System: "You must create story", Task: "Create some interesting long story"), set as entrypoint, connected to END, saved
- Pipeline open on Configuration tab → Flow View

## Test Data

- Pipeline name: "Test Pipeline — Chipset and History"
- Chat input: "run"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Verify no runs exist. Check Flow View for History Icon. | No History Icon present. No run chipsets visible. |
| 2 | Type "run" in the chat input field (bottom-right of Configuration page). Press Enter. | Pipeline starts. Run chipset appears immediately with blue loading icon and label "Run 1". |
| 3 | Wait for Run 1 to complete. Observe chipset. | Icon changes to green checkmark. "Run 1" label remains. |
| 4 | Check for History Icon in Flow View. | History Icon is NOT present (only 1 run exists). |
| 5 | Type "run" in chat input. Press Enter for Run 2. Wait for completion. | Run 2 chipset shows blue loading → green checkmark. "Run 2" displayed. |
| 6 | Check for History Icon in Flow View. | History Icon NOW appears at the top-left of Flow View, next to the current run chipset. |
| 7 | Verify Run 2 is displayed separately next to the History Icon (not grouped inside it). | Run 2 chipset is visible alongside History Icon, outside the history group. |
| 8 | Type "run" in chat input. Press Enter for Run 3. Wait for completion. | Run 3 becomes the current run. Run 3 chipset shows green checkmark and "Run 3". |
| 9 | Click the History Icon. | A grouped list opens showing previous runs. |
| 10 | Verify list contents. | List contains Run 1 (green checkmark) and Run 2 (green checkmark). Run 3 (current) is NOT in the list. |
| 11 | Close the history list. | List closes. Flow View shows Run 3 chipset and History Icon. |

## Expected Final State

List closes. Flow View shows Run 3 chipset and History Icon.

## Pass/Fail Criteria

**Pass:**
- Run chipset appears on every execution with correct icon and run number
- History Icon absent with fewer than 2 runs, present at 2+ runs
- Current run always displayed separately from history group
- History list contains only previous completed runs; current run excluded

**Fail:**
- Chipset missing icon or run number label
- History Icon appears with fewer than 2 runs, or fails to appear at exactly 2 runs
- Current run appears inside history list
- History list shows wrong runs or missing entries
