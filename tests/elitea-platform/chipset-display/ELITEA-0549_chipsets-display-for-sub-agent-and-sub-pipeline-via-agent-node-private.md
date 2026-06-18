---
id: ELITEA-0549
title: "Chipsets Display for Sub-Agent and Sub-Pipeline via Agent Node — Private and Team Projects"
priority: critical
type: functional
module: chipset-display
status: ready
execution_type: manual
tags: [eng:frontend]
requirements: [EliteaAI/elitea_issues#4503]
---
# ELITEA-0549: Chipsets Display for Sub-Agent and Sub-Pipeline via Agent Node — Private and Team Projects

**Module:** Chipset Display · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that chipsets for a sub-agent and sub-pipeline triggered via an Agent Node are displayed in the pipeline execution flow in both Private and Team projects.

**Coverage:**
- Sub-agent chipset visible in execution flow (Private & Team project)
- Sub-pipeline chipset visible in execution flow (Private & Team project)
- Chipset appears before tool/LLM call chips

## Preconditions

- Logged in to {{base_url}}
- Access to a Private project and a Team project
- A sub-agent and a sub-pipeline exist and are runnable in both projects
- Browser: latest Chrome

## Test Data

- Sub-agent: any existing agent in the project
- Sub-pipeline: any existing pipeline in the project

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | In Private project, create a pipeline with an Agent Node set to execute a sub-agent. Run it. | Chipset for the sub-agent is shown in the execution flow before tool/LLM chips. |
| 2 | Change the Agent Node to execute a sub-pipeline instead. Run the pipeline. | Chipset for the sub-pipeline is shown in the execution flow before its inner calls. |
| 3 | Repeat steps 1–2 in a Team project. | Same chipset behavior — sub-agent and sub-pipeline chipsets are both displayed correctly in the execution flow. |

## Expected Final State

Same chipset behavior — sub-agent and sub-pipeline chipsets are both displayed correctly in the execution flow.

## Pass/Fail Criteria

**Pass:**
- Chipsets for sub-agent and sub-pipeline appear in execution flow in both Private and Team projects
- Chipsets appear before tool/LLM call chips

**Fail:**
- Any chipset is missing from the execution flow (bug condition)
- Behavior differs between Private and Team project
