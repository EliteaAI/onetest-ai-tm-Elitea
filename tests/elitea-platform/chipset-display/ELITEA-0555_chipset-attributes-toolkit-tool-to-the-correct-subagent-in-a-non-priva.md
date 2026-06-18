---
id: ELITEA-0555
title: "Chipset Attributes Toolkit Tool to the Correct Subagent in a Non-Private Project"
priority: critical
type: functional
module: chipset-display
status: draft
execution_type: manual
tags: [eng:frontend, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3783]
---
# ELITEA-0555: Chipset Attributes Toolkit Tool to the Correct Subagent in a Non-Private Project

**Module:** Chipset Display · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that when a toolkit tool is triggered by one specific subagent inside a non-private project with multiple sibling subagents, the chipset displays the name of the subagent that actually fired the tool — not an arbitrary sibling.

**Coverage:**
- Non-private project as execution context
- Parent agent with 3 sibling subagents at the same level (fan-out topology)
- Only SubAgent3 has a toolkit configured; SubAgent1 and SubAgent2 do not
- Toolkit tool is triggered during the run
- Chipset label correctly names SubAgent3 as the triggering entity
- Chipset does NOT show SubAgent1 or SubAgent2 in the toolkit chipset
- Consistent attribution across 3 consecutive runs

## Preconditions

- Logged in to {{base_url}}
- A **non-private** project exists and is selected (project visibility set to non-private)
- Chromium-based browser (latest)
- At least one toolkit credential (e.g., GitHub or Jira) is available in the project

## Test Data

- Parent agent name: `BugVerifyParentAgent`
- SubAgent1 name: `SubAgent1` — no toolkit
- SubAgent2 name: `SubAgent2` — no toolkit
- SubAgent3 name: `SubAgent3` — has a toolkit (e.g., GitHub toolkit) with at least 1 tool enabled
- Prompt: one that explicitly routes execution to SubAgent3 and triggers its toolkit tool (e.g., "Use SubAgent3 to list GitHub repositories")
- Project visibility: non-private

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the non-private project. Navigate to Agents. Create a new agent named `BugVerifyParentAgent`. | Parent agent detail page opens successfully. |
| 2 | Add `SubAgent1` as a subagent to `BugVerifyParentAgent`. Ensure no toolkit is configured on SubAgent1. | SubAgent1 is attached. No toolkit visible on SubAgent1. |
| 3 | Add `SubAgent2` as a subagent to `BugVerifyParentAgent`. Ensure no toolkit is configured on SubAgent2. | SubAgent2 is attached. No toolkit visible on SubAgent2. |
| 4 | Add `SubAgent3` as a subagent to `BugVerifyParentAgent`. Add a toolkit (e.g., GitHub) to SubAgent3 with at least 1 tool enabled. | SubAgent3 is attached with the toolkit visible and configured. |
| 5 | Open the Chat tab for `BugVerifyParentAgent`. Send the prompt: "Use SubAgent3 to list GitHub repositories". | Run starts. Execution trace begins appearing in the chat. |
| 6 | Wait for the toolkit tool to fire. Observe the chipset label displayed in the execution trace for the toolkit call. | Chipset label reads `<Toolkit>: <tool> (SubAgent3)`. Neither `SubAgent1` nor `SubAgent2` appear in the toolkit chipset. |
| 7 | Repeat the same run 2 more times (total 3 runs) using the same prompt. Observe the chipset label each time. | All 3 runs consistently show `<Toolkit>: <tool> (SubAgent3)` in the toolkit chipset. No arbitrary switching between sibling names occurs. |

## Expected Final State

All 3 runs consistently show `<Toolkit>: <tool> (SubAgent3)` in the toolkit chipset. No arbitrary switching between sibling names occurs.

## Pass/Fail Criteria

**Pass:**
- All 3 runs show `<Toolkit>: <tool> (SubAgent3)` in the toolkit chipset
- `SubAgent1` and `SubAgent2` never appear in the toolkit chipset
- No blank or generic label is shown in the chipset

**Fail:**
- Any run shows `SubAgent1` or `SubAgent2` in the toolkit chipset instead of `SubAgent3`
- The chipset label alternates between sibling names across runs
- The chipset label is blank or shows a generic/system-generated name
