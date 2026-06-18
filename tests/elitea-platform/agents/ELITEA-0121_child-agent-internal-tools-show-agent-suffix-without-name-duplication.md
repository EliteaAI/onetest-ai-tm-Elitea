---
id: ELITEA-0121
title: "Child Agent Internal Tools Show Agent Suffix Without Name Duplication"
priority: high
type: functional
module: agents
status: draft
execution_type: manual
tags: [nfr:usability, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3535]
---
# ELITEA-0121: Child Agent Internal Tools Show Agent Suffix Without Name Duplication

**Module:** Agents · **Priority:** High · **Type:** Functional

**Objective:** Verify that when a child agent is added as a toolkit, its internal tools display with an (AgentName) suffix, and the Smart tool uses "Smart tool" as prefix — NOT the agent name — preventing duplicate name display.

**Coverage:**
- Smart tool chipset: prefix is "Smart tool" (not "Repository Analyst"), suffix is "(Repository Analyst)"
- Agent name does NOT appear twice in Smart tool chipset label
- Planner chipsets from child agent all carry "(Repository Analyst)" suffix
- Parent agent's own internal tools show NO parenthetical suffix

## Preconditions

- Logged in to ELITEA at {{base_url}}
- Parent Agent "ChipsetAgent" exists with child Agent "Repository Analyst" added as a toolkit
- "Repository Analyst" has Planner and Smart tool enabled internally
- Browser: Chrome/Edge latest

## Test Data

- Parent Agent: ChipsetAgent
- Child Agent toolkit: Repository Analyst (with Planner + Smart tool enabled)
- Smart tool expected label: "Smart tool: get_tools_schema (Repository Analyst)"
- Wrong format (fail): "Repository Analyst: get_tools_schema (Repository Analyst)"
- Test prompt: "Use the Repository Analyst to describe what tools are available"
- URL: {{base_url}}

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Log in to ELITEA. Navigate to Agents in the left sidebar. Open ChipsetAgent. | ChipsetAgent detail page loads. |
| 2 | Open the agent's Settings / Toolkits section. Verify that Repository Analyst is listed as an added child-agent toolkit. | Repository Analyst appears in the toolkits list with an agent-type icon. |
| 3 | Switch to the Chat or Run tab. Enter a prompt that causes ChipsetAgent to delegate to Repository Analyst (e.g., 'Use the Repository Analyst to describe what tools are available'). Press Send. | ChipsetAgent processes the prompt and invokes Repository Analyst; nested execution begins. |
| 4 | Wait for the full execution to complete. Open the thinking steps / execution trace panel. | Execution trace shows chipsets from both the parent agent's and child agent's tool calls. |
| 5 | In the execution trace, find the Smart tool chipset corresponding to a child-agent action (e.g., get_tools_schema). Read the complete label — prefix, action name, and any parenthetical suffix. | The chipset is visible with a label. |
| 6 | Verify the prefix of the Smart tool chipset is 'Smart tool' — NOT 'Repository Analyst'. | Label prefix reads 'Smart tool' (not the agent name). |
| 7 | Verify the full Smart tool chipset label reads 'Smart tool: get_tools_schema (Repository Analyst)'. Confirm the agent name does NOT appear twice (i.e., label is NOT 'Repository Analyst: get_tools_schema (Repository Analyst)'). | Agent name appears exactly once — only as the '(Repository Analyst)' parenthetical suffix at the end. |
| 8 | Locate a Planner chipset from the child agent (e.g., start_step). Read the full label. | Label reads 'Planner: start_step (Repository Analyst)' — Planner is the prefix; '(Repository Analyst)' is the suffix. |
| 9 | Repeat for update_plan and complete_step Planner chipsets. Verify each carries the (Repository Analyst) suffix consistently. | All Planner chipsets from the child agent carry the '(Repository Analyst)' suffix without exception. |
| 10 | If ChipsetAgent itself triggers its own Planner or internal tool steps, locate those chipsets in the trace. Verify they show NO parenthetical suffix (e.g., label reads 'Planner: start_step' with nothing appended). | Parent agent's own internal tool chipsets have no '(AgentName)' suffix — suffix appears only for child agent tool calls. |

## Expected Final State

Parent agent's own internal tool chipsets have no '(AgentName)' suffix — suffix appears only for child agent tool calls.

## Pass/Fail Criteria

**Pass:**
- Smart tool chipset reads "Smart tool: get_tools_schema (Repository Analyst)" — agent name appears once, only as suffix
- All child agent Planner chipsets carry "(Repository Analyst)" suffix (e.g., "Planner: start_step (Repository Analyst)")
- Parent agent's own internal tools show no parenthetical suffix

**Fail:**
- Smart tool chipset reads "Repository Analyst: get_tools_schema (Repository Analyst)" — agent name duplicated
- Any child agent Planner chipset missing the "(Repository Analyst)" suffix
- Parent agent internal tools incorrectly show an "(AgentName)" suffix
