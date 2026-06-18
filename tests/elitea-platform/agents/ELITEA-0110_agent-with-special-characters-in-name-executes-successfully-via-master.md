---
id: ELITEA-0110
title: "Agent with special characters in name executes successfully via Master Agent (GPT & Anthropic)"
priority: high
type: functional
module: agents
status: ready
execution_type: manual
tags: [issue:3875, r-2.0.1, bug]
requirements: [ProjectAlita/projectalita.github.io#3875]
---
# ELITEA-0110: Agent with special characters in name executes successfully via Master Agent (GPT & Anthropic)

**Module:** Agents · **Priority:** High · **Type:** Functional

**Objective:** Verify that an agent whose name contains special characters (`~!@#$%^&*()_+\`1-=[];'\,./`) can be saved, added to a master agent, and executed without errors using both GPT and Anthropic models.

**Coverage:**
- Agent creation with name containing the full special-character set `~!@#$%^&*()_+\`1-=[];'\,./`
- Agent saved successfully
- Special-character-named agent added as a sub-agent to a master agent
- Master agent execution with GPT model completes without errors
- Master agent execution with Anthropic model completes without errors

## Preconditions

- Logged in to {{base_url}} with a valid user account
- Access to a project with at least Editor role
- An existing master agent is available (or can be created during the test)
- Both GPT model (e.g., gpt-4o) and Anthropic model (e.g., claude-3-5-sonnet) are available in the environment

## Test Data

- Agent name: ~!@#$%^&*()_+`1-=[];'\,./
- GPT model: gpt-4o (or gpt-4)
- Anthropic model: claude-3-5-sonnet (or claude-3-opus)
- Master agent name: master_agent (existing or newly created)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the Agents section from the sidebar. | Agents list page is displayed. |
| 2 | Click 'Create Agent' (or equivalent button to create a new agent). | Agent creation form opens. |
| 3 | Enter the agent name: ~!@#$%^&*()_+`1-=[];'\,./ | Name is accepted and visible in the name field without any immediate validation error. |
| 4 | Fill in any other required fields (e.g., description, system prompt, model) and click Save. | Agent is saved successfully. No error is displayed. The agent appears in the agents list. |
| 5 | Open or create a master agent. | Master agent edit page is displayed. |
| 6 | Add the newly created special-character-named agent as a sub-agent/tool to the master agent. | The special-character-named agent appears in the master agent's tool/agent list. |
| 7 | Save the master agent. | Master agent is saved successfully without errors. |
| 8 | Select a GPT model (e.g., gpt-5 mini) for the master agent and execute it with a test prompt. | Master agent executes without errors. A valid response is returned. |
| 9 | Switch to an Anthropic model (e.g., claude-4.5-sonnet) for the master agent and execute it with a test prompt. | Master agent executes without errors. A valid response is returned. No error related to agent name or tool name sanitization appears. |

## Expected Final State

Master agent executes without errors. A valid response is returned. No error related to agent name or tool name sanitization appears.

## Pass/Fail Criteria

**Pass:**
- Agent with special characters in name is saved successfully
- Special-character-named agent is added to master agent without issues
- Master agent executes successfully with GPT model and returns a response
- Master agent executes successfully with Anthropic model and returns a response
- No errors appear at any step

**Fail:**
- Agent cannot be saved due to name containing special characters
- Master agent fails to execute with either GPT or Anthropic model
- An error related to tool name sanitization or agent name parsing appears during execution
- Any unexpected error message is displayed
