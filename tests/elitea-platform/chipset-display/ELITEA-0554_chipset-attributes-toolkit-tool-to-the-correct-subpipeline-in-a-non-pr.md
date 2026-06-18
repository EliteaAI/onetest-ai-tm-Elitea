---
id: ELITEA-0554
title: "Chipset Attributes Toolkit Tool to the Correct Subpipeline in a Non-Private Project"
priority: critical
type: functional
module: chipset-display
status: draft
execution_type: manual
tags: [eng:frontend, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3783]
---
# ELITEA-0554: Chipset Attributes Toolkit Tool to the Correct Subpipeline in a Non-Private Project

**Module:** Chipset Display · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that when a toolkit tool is triggered by one specific subpipeline inside a non-private project with multiple sibling subpipelines, the chipset displays the name of the subpipeline that actually fired the tool — not an arbitrary sibling.

**Coverage:**
- Non-private project as execution context
- Parent pipeline with 3 sibling subpipelines at the same level (fan-out topology)
- Only SubPipeline3 has a toolkit configured; SubPipeline1 and SubPipeline2 do not
- Toolkit tool is triggered during the run
- Chipset label correctly names SubPipeline3 as the triggering entity
- Chipset does NOT show SubPipeline1 or SubPipeline2 in the toolkit chipset
- Consistent attribution across 3 consecutive runs

## Preconditions

- Logged in to {{base_url}}
- A **non-private** project exists and is selected (project visibility set to non-private)
- Chromium-based browser (latest)
- At least one toolkit credential (e.g., GitHub or Jira) is available in the project

## Test Data

- Parent pipeline name: `BugVerifyParentPipeline`
- SubPipeline1 name: `SubPipeline1` — no toolkit
- SubPipeline2 name: `SubPipeline2` — no toolkit
- SubPipeline3 name: `SubPipeline3` — has a toolkit (e.g., GitHub toolkit) with at least 1 tool enabled
- Prompt: one that explicitly routes execution to SubPipeline3 and triggers its toolkit tool (e.g., "Use SubPipeline3 to list GitHub repositories")
- Project visibility: non-private

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the non-private project. Navigate to Pipelines. Create a new pipeline named `BugVerifyParentPipeline`. | Parent pipeline detail page opens successfully. |
| 2 | Add `SubPipeline1` as a nested subpipeline to `BugVerifyParentPipeline`. Ensure no toolkit is configured on SubPipeline1. | SubPipeline1 is attached. No toolkit visible on SubPipeline1. |
| 3 | Add `SubPipeline2` as a nested subpipeline to `BugVerifyParentPipeline`. Ensure no toolkit is configured on SubPipeline2. | SubPipeline2 is attached. No toolkit visible on SubPipeline2. |
| 4 | Add `SubPipeline3` as a nested subpipeline to `BugVerifyParentPipeline`. Add a toolkit (e.g., GitHub) to SubPipeline3 with at least 1 tool enabled. | SubPipeline3 is attached with the toolkit visible and configured. |
| 5 | Open the Chat tab for `BugVerifyParentPipeline`. Send the prompt: "Use SubPipeline3 to list GitHub repositories". | Run starts. Execution trace begins appearing in the chat. |
| 6 | Wait for the toolkit tool to fire. Observe the chipset label displayed in the execution trace for the toolkit call. | Chipset label reads `<Toolkit>: <tool> (SubPipeline3)`. Neither `SubPipeline1` nor `SubPipeline2` appear in the toolkit chipset. |
| 7 | Repeat the same run 2 more times (total 3 runs) using the same prompt. Observe the chipset label each time. | All 3 runs consistently show `<Toolkit>: <tool> (SubPipeline3)` in the toolkit chipset. No arbitrary switching between sibling names occurs. |

## Expected Final State

All 3 runs consistently show `<Toolkit>: <tool> (SubPipeline3)` in the toolkit chipset. No arbitrary switching between sibling names occurs.

## Pass/Fail Criteria

**Pass:**
- All 3 runs show `<Toolkit>: <tool> (SubPipeline3)` in the toolkit chipset
- `SubPipeline1` and `SubPipeline2` never appear in the toolkit chipset
- No blank or generic label is shown in the chipset

**Fail:**
- Any run shows `SubPipeline1` or `SubPipeline2` in the toolkit chipset instead of `SubPipeline3`
- The chipset label alternates between sibling names across runs
- The chipset label is blank or shows a generic/system-generated name
