---
id: ELITEA-0818
title: "Agent Node UI Displays Empty Field (Not []) When chat_history Is Cleared and Absent from YAML"
priority: critical
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [feat:pipeline_nodes, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3827]
---
# ELITEA-0818: Agent Node UI Displays Empty Field (Not []) When chat_history Is Cleared and Absent from YAML

**Module:** Pipelines · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that when the `chat_history` field in an Agent Node is cleared and saved, the UI displays an empty/blank field — not `[]` — accurately reflecting the actual absent value in the YAML `input_mapping`.

**Coverage:**
- Clearing `chat_history` value in the Agent Node config panel and saving results in UI showing an empty/blank field (not `[]`)
- YAML `input_mapping` has `chat_history` absent after clearing
- UI and YAML remain in sync after save: what is displayed in the node UI matches what is in the YAML
- Re-entering `[]` explicitly and saving correctly shows `[]` in both UI and YAML
- UI does not show stale/incorrect value after node save

## Preconditions

- Logged in at {{base_url}}
- Private project with pipeline creation rights
- At least one Agent configured in the project Toolkits
- Chromium-based browser (latest)

## Test Data

- Pipeline name: `TC-ChatHistoryClear`
- Agent Node: any valid Agent assigned
- `task` field: Type = Fixed, Value = `Run`
- `chat_history` field initial value: `[]` (explicitly set)
- Expected display after clearing: empty/blank field — NOT `[]`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Create pipeline `TC-ChatHistoryClear`. Add an Agent Node connected to End. Assign a valid Agent. In the node config panel, set the `task` field to Fixed type with value `Run`. Set `chat_history` to Fixed type with value `[]`. Click Save. | Pipeline saves. `chat_history` shows `[]` in the node config UI. |
| 2 | Click the YAML View tab. Locate the Agent Node's `input_mapping` section. | YAML contains `chat_history: []` — field is present and explicitly set. |
| 3 | Switch back to Flow View. Click the Agent Node to open its config panel. In the `chat_history` field, clear the current value (delete `[]`, leaving the field blank). Click Save. | Pipeline saves without error. |
| 4 | Click the Agent Node again to reopen the config panel. Observe the `chat_history` field value displayed in the UI. | `chat_history` field shows empty/blank — NOT `[]`. The UI accurately reflects the absent/unset state. |
| 5 | Click the YAML View tab. Inspect the `input_mapping` section for the Agent Node. | The `chat_history` key is absent from `input_mapping`. There is no `chat_history: []` entry in the YAML. |
| 6 | Switch back to Flow View. Reopen the Agent Node config. Re-enter `[]` in the `chat_history` field. Click Save. Reopen the node config. | `chat_history` field now shows `[]` again — correctly reflecting the explicitly set empty array. |
| 7 | Click the YAML View tab. Inspect `input_mapping`. | YAML contains `chat_history: []` — field is present and matches what the UI displays. UI and YAML are in sync. |

## Expected Final State

YAML contains `chat_history: []` — field is present and matches what the UI displays. UI and YAML are in sync.

## Pass/Fail Criteria

**Pass:**
- After clearing and saving, UI shows an empty/blank `chat_history` field — not `[]`
- YAML confirms the field is absent when the UI value is cleared
- UI and YAML are in sync at all times: what UI shows matches what is in the YAML
- Re-entering `[]` explicitly and saving correctly restores `chat_history: []` in both UI and YAML

**Fail:**
- After clearing and saving, UI still displays `[]` while YAML has the field absent (the original bug — stale/incorrect UI display)
- UI and YAML are out of sync after save
- Explicitly setting `[]` does not persist to the YAML `input_mapping`
