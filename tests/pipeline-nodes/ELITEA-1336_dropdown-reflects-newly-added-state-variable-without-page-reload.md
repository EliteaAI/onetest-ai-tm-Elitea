---
id: ELITEA-1336
title: "Dropdown Reflects Newly Added State Variable Without Page Reload"
priority: high
type: functional
module: pipeline-nodes
status: ready
execution_type: manual
tags: [feat:pipelines, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#2626]
---
# ELITEA-1336: Dropdown Reflects Newly Added State Variable Without Page Reload

**Module:** Pipeline Nodes · **Priority:** High · **Type:** Functional

**Objective:** Verify that after adding a new state variable to the pipeline, the F-String dropdown immediately includes it — no page reload required.

**Coverage:**
- New state variable added via States sidebar appears in dropdown instantly
- Newly added variable is selectable and inserts correctly

## Preconditions

- Logged into {{base_url}}
- Pipeline with only default state variables (`input`, `messages`) — no custom variables
- LLM node with Task field set to F-String

## Test Data

New state variable: `new_result` (type: str)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the LLM node Task field (F-String). Type `{`. Confirm only `input` and `messages` appear in the dropdown. Press Escape. | Dropdown shows exactly 2 variables: `input` and `messages`. |
| 2 | Open the States sidebar. Click `+ Context`. Enter variable name `new_result`, set type to `str`. Save. | `new_result` appears in the States sidebar. No page reload performed. |
| 3 | Return to the LLM node Task field (F-String). Type `{`. | Dropdown now shows `input`, `messages`, and `new_result` — all 3 variables listed without page reload. |
| 4 | Select `new_result` from the dropdown. | `{new_result}` is inserted into the Task field correctly. |

## Expected Final State

`{new_result}` is inserted into the Task field correctly.

## Pass/Fail Criteria

**Pass:**
- Newly added `new_result` appears in the dropdown immediately without page reload
- Variable inserts correctly as `{new_result}`

**Fail:**
- `new_result` not visible in dropdown until page is reloaded
- Insertion fails or is malformed
