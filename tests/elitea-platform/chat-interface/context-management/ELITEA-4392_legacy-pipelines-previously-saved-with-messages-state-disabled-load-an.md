---
id: ELITEA-4392
title: "Legacy Pipelines Previously Saved With 'Messages' State Disabled Load and Run Correctly After the Fix"
priority: critical
type: functional
module: context-management
status: draft
execution_type: manual
tags: [feat:chat, feat:context-management, feat:pipelines, issue:4840, r-2.0.8]
requirements: [EliteaAI/elitea_issues#4840]
---
# ELITEA-4392: Legacy Pipelines Previously Saved With 'Messages' State Disabled Load and Run Correctly After the Fix

**Module:** Context Management · **Priority:** Critical · **Type:** Functional

**Objective:** Verify backward compatibility: if the fix removes or forces-on the "messages" state toggle, pre-existing pipelines that were saved with "messages" disabled continue to open, run, and participate in chat without data corruption or execution failure.

## Preconditions

- Logged in to {{base_url}}
- A pipeline created/saved before the fix with "messages" state explicitly disabled exists in the environment

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Pipeline | Legacy pipeline saved pre-fix with "messages" state disabled |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the legacy pipeline (saved with "messages" disabled) in the Pipeline editor. | Pipeline editor opens without error; no load failure or corrupted configuration warning. |
| 2 | Open the STATE panel and verify how the "messages" variable is now displayed (forced ON, toggle removed/disabled, or migrated value). | The "messages" variable displays a valid, expected state (either still togglable and correctly reflecting its prior value, or forced ON/migrated per the fix design) — no broken or missing state entry. |
| 3 | Save the pipeline (if any change is required) and verify no errors occur. | Save completes successfully with no error toast or validation failure. |
| 4 | Run the pipeline directly from the Pipeline page and verify successful execution with correct state behavior. | Pipeline executes successfully; state behavior (messages accumulation) is correct. |
| 5 | Add the same legacy pipeline as a chat participant, run it, deselect it, and send a follow-up message. | All actions complete without error; pipeline behaves as a normal chat participant. |
| 6 | Verify the Context Budget values behave correctly (no inflation) throughout. | Messages/token counts remain accurate at every step — no inflated count after deselect, consistent with the fix for issue #4840. |
| 7 | Verify the pipeline's YAML definition reflects the updated/migrated state configuration without corrupting other state variables (input, tool_outcomes, last_tool_outcome, custom variables). | YAML shows the correct "messages" state configuration post-migration; all other state variables (input, tool_outcomes, last_tool_outcome, custom variables) remain intact and unmodified. |

## Expected Final State

The legacy pipeline opens, saves, runs, and participates in chat correctly post-fix, with its "messages" state migrated/handled appropriately and all other state variables preserved without corruption.

## Pass/Fail Criteria

**Pass:**
- Legacy pipeline loads, saves, and runs without error.
- "Messages" state displays and behaves correctly (migrated/forced-on/preserved as per fix design).
- Context Budget values remain correct throughout chat participation.
- YAML definition shows no corruption to other state variables.

**Fail:**
- Legacy pipeline fails to load, save, or run.
- "Messages" state is missing, broken, or displays an invalid value.
- Context Budget inflates after deselecting the pipeline.
- Other state variables (input, tool_outcomes, last_tool_outcome, custom variables) are corrupted or lost after migration.
