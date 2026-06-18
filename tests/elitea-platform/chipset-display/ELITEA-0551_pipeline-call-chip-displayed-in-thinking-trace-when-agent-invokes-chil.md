---
id: ELITEA-0551
title: "Pipeline Call Chip Displayed in Thinking Trace When Agent Invokes Child Pipeline — Team Project"
priority: high
type: functional
module: chipset-display
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.2]
requirements: [EliteaAI/elitea_issues#4388]
---
# ELITEA-0551: Pipeline Call Chip Displayed in Thinking Trace When Agent Invokes Child Pipeline — Team Project

**Module:** Chipset Display · **Priority:** High · **Type:** Functional

**Objective:** Verify that after the fix, when a parent agent in a Team project invokes a child pipeline, a pipeline chip (with pipeline icon and pipeline name) appears in the thinking trace before the inner pipeline nodes/tools chips.

**Coverage:**
- Pipeline call chip presence in the thinking trace in a Team project
- Pipeline chip shows correct pipeline icon and pipeline name
- Pipeline chip appears before the first node/tool chip from the child pipeline
- Trace order: agent steps → pipeline chip → inner pipeline node chips

## Preconditions

- Logged in to {{base_url}}
- Team project with a parent agent that has a child pipeline attached as a toolkit (e.g., `ParentAIAssistantAgent`)

## Test Data

- Project type: Team
- Parent agent: one with a child pipeline configured as a toolkit
- Child pipeline: any pipeline with at least one node/tool

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the Team project → Agents. Open the parent agent and run it so the child pipeline is invoked. | Execution starts and completes. |
| 2 | Open the thinking trace / chipset in the run view. | The trace is visible. |
| 3 | Inspect the chips in order of execution. | A pipeline chip appears before the first node/tool chip from the child pipeline. The pipeline chip shows the pipeline icon and the pipeline name. |
| 4 | Confirm no inner pipeline node/tool chip appears without the preceding pipeline chip. | The trace order is correct: agent steps → pipeline chip → inner pipeline nodes/tools. |

## Expected Final State

The trace order is correct: agent steps → pipeline chip → inner pipeline nodes/tools.

## Pass/Fail Criteria

**Pass:**
- Pipeline chip with pipeline icon and name is present in the trace
- Pipeline chip appears before any inner pipeline node/tool chips

**Fail:**
- Pipeline chip is absent — trace jumps directly to inner pipeline node/tool chips
- Pipeline chip has no icon or no name
- Chips appear in incorrect order
