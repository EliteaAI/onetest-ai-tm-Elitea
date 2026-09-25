---
id: ELITEA-3423
title: "System State Variables tool_outcomes/last_tool_outcome Present on a Brand-New, Never-Run Pipeline"
priority: high
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [feat:pipelines, state-variables, story:6593, reserved-variables, regression]
requirements: [EliteaAI/elitea_issues#6593]
---
# ELITEA-3423: System State Variables Present on a Brand-New, Never-Run Pipeline

**Module:** Pipelines · **Priority:** High · **Type:** Functional

**Objective:** Confirm `tool_outcomes` and `last_tool_outcome` render as default, read-only state-variable rows on a pipeline that has just been created and never run — the same way `input` and `messages` already do — per the reporter's own clarifying comment on #6593 ("For all new pipelines, we need to add these 2 state variables as defaults (similar to input and messages)").

**Coverage:** AC / regression — the merged UI only appears to add a reserved-name row once `states?.[name]` is populated by a tool execution; this case checks the "from creation" requirement directly rather than the "after a tool runs" fallback.

## Preconditions

- User has permission to create pipelines in the current project
- No pipeline named for this test already exists

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Create a new, empty pipeline and open its flow editor. | Pipeline opens with the default STATE panel. |
| 2 | Open the STATE panel without adding any tool node and without running the pipeline. | `input` and `messages` rows are visible, as usual. |
| 3 | Inspect the STATE panel for `tool_outcomes` and `last_tool_outcome` rows. | Both rows are present immediately, styled as read-only/default (no delete affordance, no editable name field), same visual pattern as `input`/`messages`. |
| 4 | Check the type shown for each of the two rows. | Both show type `dict`/JSON. |

## Expected Final State

A pipeline that has never been run already shows `tool_outcomes` and `last_tool_outcome` as default, read-only, JSON-typed state variables — identical in presence/timing to `input` and `messages`.

## Pass/Fail Criteria

**Pass:**
- Both rows are visible in step 3 on the never-run pipeline, with read-only styling and JSON type

**Fail:**
- Either row is absent until a tool node has actually executed (current implementation gates row rendering on `states?.[name]` being truthy) — file as a gap against #6593's own stated intent
