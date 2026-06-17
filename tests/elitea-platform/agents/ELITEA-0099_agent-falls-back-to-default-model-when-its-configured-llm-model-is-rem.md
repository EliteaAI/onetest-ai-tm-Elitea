---
id: ELITEA-0099
title: "Agent falls back to default model when its configured LLM model is removed from the project"
priority: medium
type: functional
module: agents
status: ready
execution_type: manual
tags: [eng:migration, issue:3877, r-2.0.1, bug]
requirements: [ProjectAlita/projectalita.github.io#3877]
---
# ELITEA-0099: Agent falls back to default model when its configured LLM model is removed from the project

**Module:** Agents · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that when an LLM model is removed from the environment/project models list, an agent (used directly or as a nested agent) automatically falls back to the default model instead of continuing to use the removed model.

**Coverage:**
- Agent configured with a specific LLM model
- LLM model removed from the environment/project models list
- Agent executed directly — default model is used
- Agent used as a nested agent inside a master agent — default model is used
- No error or broken execution caused by the missing model reference

## Preconditions

- Logged in to {{base_url}} with a valid user account with project admin access
- A specific LLM model is available in the project/environment models list
- A master agent and a nested agent exist (or can be created) in the project

## Test Data

- Nested agent LLM model: any model available in the project (e.g., gpt-4o)
- Default model: the fallback model configured in the project/environment settings
- Master agent: any agent with the nested agent attached

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the Agents page. Create or open an existing agent. Set it to use a specific LLM model (e.g., gpt-4o). Save the agent. | Agent is saved with the specific LLM model configured. |
| 2 | Add this agent as a nested agent to a master agent. Save the master agent. | Master agent is saved with the nested agent attached. |
| 3 | Navigate to project/environment Settings. Remove the LLM model used by the nested agent from the models list. | The LLM model is removed from the project/environment models list. |
| 4 | Open the nested agent directly and execute it with a test prompt. | Agent executes successfully using the default model. The removed model is not used. |
| 5 | Open the master agent and execute it with a test prompt. | Master agent executes successfully. The nested agent uses the default model (not the removed one). No error referencing the removed model is shown. |

## Expected Final State

Master agent executes successfully. The nested agent uses the default model (not the removed one). No error referencing the removed model is shown.

## Pass/Fail Criteria

**Pass:**
- Agent falls back to the default model when its configured LLM model has been removed
- Master agent executes successfully using the default model for the nested agent
- No error referencing the removed model is shown

**Fail:**
- Nested agent continues to use the removed LLM model
- Execution fails or produces an unexpected error due to the missing model
