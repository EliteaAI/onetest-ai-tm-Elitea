---
id: ELITEA-0550
title: "Pipeline Call Chip Displayed in Thinking Trace When Agent Invokes Child Pipeline — Private Project (Regression)"
priority: high
type: functional
module: chipset-display
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.2]
requirements: [EliteaAI/elitea_issues#4388]
---
# ELITEA-0550: Pipeline Call Chip Displayed in Thinking Trace When Agent Invokes Child Pipeline — Private Project (Regression)

**Module:** Chipset Display · **Priority:** High · **Type:** Functional

**Objective:** Verify the fix does not regress pipeline call chip display in Private projects, and that the pipeline chip appears correctly in the thinking trace in Private project agent runs.

**Coverage:**
- Pipeline chip presence in thinking trace in a Private project (regression)
- Correct chip order: pipeline chip before inner pipeline node chips
- No new regressions introduced by the fix

## Preconditions

- Logged in to {{base_url}}
- Private project with a parent agent that has a child pipeline attached as a toolkit

## Test Data

- Project type: Private
- Parent agent: one with a child pipeline configured as a toolkit
- Child pipeline: any pipeline with at least one node/tool

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the Private project → Agents. Open the parent agent and run it so the child pipeline is invoked. | Execution starts and completes. |
| 2 | Open the thinking trace / chipset in the run view. | The trace is visible. |
| 3 | Inspect the chips in order of execution. | A pipeline chip with pipeline icon and pipeline name appears before the first node/tool chip from the child pipeline. |
| 4 | Confirm trace order is correct end-to-end. | No regression — pipeline chip is shown correctly, inner pipeline nodes follow after it. |

## Expected Final State

No regression — pipeline chip is shown correctly, inner pipeline nodes follow after it.

## Pass/Fail Criteria

**Pass:**
- Pipeline chip with icon and name present and in correct position in Private project trace
- No regression to previously correct behavior

**Fail:**
- Pipeline chip missing in Private project after the fix is deployed
- Any regression to previously correct behavior
