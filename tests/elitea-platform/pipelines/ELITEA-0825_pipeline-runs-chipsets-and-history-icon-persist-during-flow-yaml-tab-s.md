---
id: ELITEA-0825
title: "Pipeline Runs — Chipsets and History Icon Persist During Flow / YAML Tab Switching"
priority: medium
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [feat:pipelines, story:2186]
requirements: [ProjectAlita/projectalita.github.io#2186]
---
# ELITEA-0825: Pipeline Runs — Chipsets and History Icon Persist During Flow / YAML Tab Switching

**Module:** Pipelines · **Priority:** Medium · **Type:** Functional

**Objective:** Verify pipeline run chipsets, the History Icon, and run numbers remain visible and accessible after switching between the Flow View and YAML View tabs — with no data loss or visual regression on return.

**Coverage:**
- Run chipsets visible in both Flow View and YAML View
- History Icon present and functional in both views
- History list content consistent across both views (correct runs, correct icons)
- Current run displayed correctly in both views
- Run data identical before and after tab switch
- No runs added or lost during tab navigation

## Preconditions

- Logged in at {URL}, project {Project} selected
- Pipeline "Test Pipeline — Tab Switching" created: LLM node (System: "You must create story", Task: "Create some interesting long story"), set as entrypoint, saved
- Pipeline open on Configuration tab → Flow View
- Two completed runs (Run 1 and Run 2) already executed via chat input before starting test steps

## Test Data

- Pipeline name: "Test Pipeline — Tab Switching"
- Chat input: "run"
- Required pre-state: 2 completed runs (Run 1 and Run 2)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | In Flow View: verify History Icon present (top-left), Run 2 displayed as current run with green checkmark. | History Icon and Run 2 chipset visible. |
| 2 | Click the YAML View tab. | YAML content is displayed. |
| 3 | Verify in YAML View: History Icon still present, Run 2 chipset still displayed separately next to it. | All run UI elements persist in YAML View without any loss. |
| 4 | Click the History Icon in YAML View. | History list opens. |
| 5 | Verify list shows Run 1 with status icon; Run 2 (current) is NOT in the list. | History list content correct and consistent with what was in Flow View. |
| 6 | Close the history list. Switch back to Flow View tab. | Flow View visual editor is displayed. |
| 7 | Verify in Flow View (after return): History Icon present, Run 2 chipset present with correct status icon. | All run data identical to state before tab switch. No visual regressions. |
| 8 | Click History Icon in Flow View. Verify Run 1 in list; Run 2 not in list. | History list consistent with the YAML View state — same content, same icons. |

## Expected Final State

History list consistent with the YAML View state — same content, same icons.

## Pass/Fail Criteria

**Pass:**
- Run chipsets and History Icon visible and functional in both views
- History list content consistent across both views
- No run data changes (added or lost) during tab switching
- Visual elements render correctly in both views

**Fail:**
- Chipsets disappear after switching to YAML View or on return to Flow View
- History Icon missing in either view
- Run count changes during tab switch
- History list shows different content depending on which tab it was opened from
