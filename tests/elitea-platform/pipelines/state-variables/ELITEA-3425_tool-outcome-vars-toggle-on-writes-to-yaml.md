---
id: ELITEA-3425
title: "Toggling a System State Variable ON Writes It Into the Pipeline YAML; Toggling OFF Removes It"
priority: high
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [feat:pipelines, state-variables, story:6593, reserved-variables, yaml, regression]
requirements: [EliteaAI/elitea_issues#6593]
---
# ELITEA-3425: Toggling ON Writes the System State Variable Into the Pipeline YAML

**Module:** Pipelines · **Priority:** High · **Type:** Functional

**Objective:** Confirm that switching the `tool_outcomes` or `last_tool_outcome` toggle to ON adds that variable into the pipeline's YAML `state:` schema, and switching it back OFF removes it again — per the reporter's own clarifying comment on #6593 ("When turned on, they should be added to YAML").

**Coverage:** AC / regression — no toggle→YAML wiring was found in the merged diffs, and `elitea_core#446`'s `validate_yaml_from_str()` actively rejects a save if either reserved name appears in the `state:` block at all, which would directly conflict with this requirement if a toggle-driven write were ever attempted.

## Preconditions

- User has permission to create and save pipelines in the current project
- A pipeline exists where `tool_outcomes` and `last_tool_outcome` rows are visible with their toggle currently OFF (per [[ELITEA-3424]])
- Access to view/export the pipeline's underlying YAML (e.g. via the flow editor's YAML view or export)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | View the pipeline's YAML `state:` block before touching any toggle. | Neither `tool_outcomes` nor `last_tool_outcome` appears in the `state:` block. |
| 2 | Toggle the `tool_outcomes` row ON. | Toggle switches to ON with no error. |
| 3 | Re-view the pipeline's YAML `state:` block. | `tool_outcomes` now appears in the `state:` block, declared with a JSON/dict type. |
| 4 | Save the pipeline. | Save succeeds (no reserved-name validation error is raised for this toggle-driven write). |
| 5 | Toggle `tool_outcomes` back OFF and re-view the YAML `state:` block. | `tool_outcomes` is removed from the `state:` block again. |
| 6 | Repeat steps 2–5 for `last_tool_outcome`. | Same behavior: appears in YAML on toggle ON, removed on toggle OFF, save succeeds while ON. |

## Expected Final State

The toggle is the supported mechanism for adding/removing a reserved system variable from the pipeline's declared YAML state schema; toggling on always succeeds and is reflected in the YAML, toggling off removes it.

## Pass/Fail Criteria

**Pass:**
- Steps 3 and 6 show the toggled-on variable present in YAML
- Step 4 save succeeds
- Step 5 (and its repeat for `last_tool_outcome`) shows the variable removed from YAML after toggling off

**Fail:**
- Toggling ON has no effect on the YAML `state:` block (no wiring exists) — the most concrete, mechanically-checkable gap identified in this feature
- Toggling ON and saving raises a reserved-name validation error (the save-time guard added by this same fix would reject the very write this requirement calls for)
- Toggling OFF does not remove the variable from YAML after it was added
