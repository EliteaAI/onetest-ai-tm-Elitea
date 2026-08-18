---
id: ELITEA-2647
title: "User Override of Module State in Individual Agent"
priority: high
type: functional
module: default-modules
status: ready
execution_type: manual
tags: [feat:settings, feat:modules, feat:agents, eng:frontend, issue:6122, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6122]
---
# ELITEA-2647: User Override of Module State in Individual Agent

**Module:** Default Modules · **Priority:** High · **Type:** Functional

**Objective:** Verify that users can override the project default module states in individual Agents — enabling modules that are disabled by default and disabling modules that are enabled by default.

**Coverage:**
- User can enable modules disabled by project defaults in an Agent
- User can disable modules enabled by project defaults in an Agent
- Override persists for that specific Agent after save
- Override does not affect project defaults or other Agents

## Preconditions

- Logged into {{base_url}}
- User has permission to modify project settings and Agent configurations
- Browser: Chrome/Firefox/Edge (latest)

## Test Data

Project default configuration:
- Enabled for Agents: Python Sandbox, Swarm Mode
- Disabled for Agents: All others (including Image Creation, Planner)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Settings → General → Default Modules. | Default Modules section is displayed. |
| 2 | Configure defaults: Enable Python Sandbox and Swarm Mode for Agents, disable all others. | Configuration saved. |
| 3 | Navigate to Agents and create a new Agent ("Override Test Agent"). | Agent creation form opens. Python Sandbox and Swarm Mode are ON, others OFF. |
| 4 | In the Modules section of the Agent form, disable Python Sandbox (toggle OFF). | Python Sandbox switches to OFF for this Agent. |
| 5 | Enable Image Creation module for this Agent (toggle ON). | Image Creation switches to ON for this Agent. |
| 6 | Enable Planner module for this Agent (toggle ON). | Planner switches to ON for this Agent. |
| 7 | Fill in other required fields (name, system prompt). | Fields completed. |
| 8 | Save the Agent. | Agent saved successfully. |
| 9 | Close and reopen the Agent for editing. | Agent editor opens. |
| 10 | Verify module states in the reopened Agent. | Python Sandbox OFF, Swarm Mode ON, Image Creation ON, Planner ON. |
| 11 | Navigate to Settings → General → Default Modules. | Default Modules section displayed. |
| 12 | Verify project defaults are unchanged. | Python Sandbox and Swarm Mode still ON by default. Image Creation and Planner still OFF by default. |
| 13 | Create another new Agent ("Default Test Agent"). | Agent creation form opens. |
| 14 | Verify modules match project defaults. | Python Sandbox and Swarm Mode are ON (default), Image Creation and Planner are OFF (default). |
| 15 | Return to "Override Test Agent" and verify overrides still in place. | Overrides persisted: Python Sandbox OFF, Swarm Mode ON, Image Creation ON, Planner ON. |
| 16 | Test "Override Test Agent" by sending a message. | Agent responds correctly with its configured modules. |

## Expected Final State

- "Override Test Agent" has user-modified module states different from project defaults
- Project defaults remain unchanged
- New Agents continue to use project defaults
- Agent functions correctly with overridden module configuration

## Pass/Fail Criteria

**Pass:**
- User can enable default-disabled modules in individual Agent
- User can disable default-enabled modules in individual Agent
- Overrides persist after Agent save and reopen
- Overrides do not affect project defaults
- Other Agents continue to use project defaults
- Agent functions correctly with overridden modules

**Fail:**
- User cannot override module states in Agent
- Overrides do not persist after save
- Overrides modify project defaults
- Other Agents are affected by individual overrides
- Agent malfunctions with overridden modules
