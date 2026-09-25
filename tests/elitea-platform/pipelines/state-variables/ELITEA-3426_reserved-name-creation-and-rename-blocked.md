---
id: ELITEA-3426
title: "Creating or Renaming a State Variable to tool_outcomes/last_tool_outcome Is Blocked (UI and Backend)"
priority: high
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [feat:pipelines, state-variables, story:6593, reserved-variables, validation]
requirements: [EliteaAI/elitea_issues#6593]
---
# ELITEA-3426: Creating or Renaming a State Variable to a Reserved Name Is Blocked

**Module:** Pipelines · **Priority:** High · **Type:** Functional

**Objective:** Confirm a user cannot create a new state variable, or rename an existing one, to either reserved system name (`tool_outcomes`, `last_tool_outcome`) via the UI, and that the same restriction is enforced server-side, not just as client-side validation.

**Coverage:** AC — `validateVariableName` in the flow editor and the SDK's `create_state()` both reject the reserved names; this case confirms both the create and rename entry points, plus a direct-API bypass attempt.

## Preconditions

- User has permission to create/edit pipelines in the current project
- A pipeline exists with at least one ordinary, non-reserved state variable (e.g. `my_var`)
- API access (or a tool such as the browser network inspector / a REST client) available to call the pipeline update endpoint directly

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | In the flow editor's "add state variable" flow, type `tool_outcomes` as the new variable's name and attempt to save. | Inline validation error such as "This name is reserved for system use and cannot be created manually" is shown; Save/Create is blocked. |
| 2 | Repeat step 1 with `last_tool_outcome`. | Same validation error; blocked. |
| 3 | Select the existing `my_var` variable and attempt to rename it to `tool_outcomes`. | Same reserved-name validation error fires on rename; rename is blocked. |
| 4 | Call the pipeline create/update API directly with a state variable named `tool_outcomes` in the payload, bypassing the UI. | Request is rejected server-side with a reserved-name error (not silently accepted). |
| 5 | Attempt a near-miss bypass: create a variable named `Tool_Outcomes` (different case) or `tool_outcomes ` (trailing space). | Record actual behavior — confirm whether this is accepted (exact-string-match guard only) or also blocked; not a hard fail either way, but log the finding. |

## Expected Final State

Both reserved names are unavailable for user-created or renamed state variables through every entry point (UI create, UI rename, direct API), independent of each other.

## Pass/Fail Criteria

**Pass:**
- Steps 1–4 each block the reserved-name usage with a clear error, both client-side and server-side

**Fail:**
- Any of steps 1–4 allows a reserved name to be created, renamed into, or saved via direct API call without rejection
