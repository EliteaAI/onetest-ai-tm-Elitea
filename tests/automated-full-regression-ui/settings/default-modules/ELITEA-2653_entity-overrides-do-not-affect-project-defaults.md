---
id: ELITEA-2653
title: "Chat and Agent Module Overrides Do Not Affect Project Defaults"
priority: critical
type: functional
module: default-modules
status: draft
execution_type: manual
tags: [feat:settings, feat:modules, feat:chats, feat:agents, eng:frontend, eng:automation, issue:6122, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6122]
---
# ELITEA-2653: Chat and Agent Module Overrides Do Not Affect Project Defaults

**Module:** Default Modules · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that changing module settings in individual Chats or Agents does NOT modify the project's default module configuration. Project defaults should remain unchanged when users override modules in specific entities.

**Coverage:**
- Disabling a default-enabled module in Chat does not affect project defaults
- Enabling a default-disabled module in Chat does not affect project defaults
- Disabling a default-enabled module in Agent does not affect project defaults
- Enabling a default-disabled module in Agent does not affect project defaults
- New entities continue using project defaults after other entities have overrides

## Preconditions

- Logged into {{base_url}}
- User has permission to modify project settings, Chat modules, and Agent configurations
- Browser: Chrome/Firefox/Edge (latest)

## Test Data

Project default configuration:
- For Chats: Image Creation ON, Planner ON, all others OFF
- For Agents: Python Sandbox ON, Swarm Mode ON, all others OFF

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Settings → General → Default Modules. | Default Modules section is displayed. |
| 2 | Configure Chats defaults: Enable Image Creation and Planner, disable all others. | Configuration saved. |
| 3 | Configure Agents defaults: Enable Python Sandbox and Swarm Mode, disable all others. | Configuration saved. |
| 4 | Navigate to Chats and create a new Chat ("Override Test Chat"). | Chat created. |
| 5 | Open Modules panel in the Chat. | Image Creation and Planner are ON, others OFF. |
| 6 | Disable Image Creation in this Chat (toggle OFF). | Image Creation switches to OFF in this Chat. |
| 7 | Enable Data Analysis in this Chat (toggle ON). | Data Analysis switches to ON in this Chat. |
| 8 | Navigate to Settings → General → Default Modules. | Default Modules section displayed. |
| 9 | Verify Chats project defaults are unchanged. | Image Creation and Planner are still ON. Data Analysis is still OFF. |
| 10 | Create another new Chat ("Verify Defaults Chat"). | Chat created. |
| 11 | Open Modules panel in new Chat. | Image Creation and Planner are ON (project defaults), Data Analysis is OFF. |
| 12 | Navigate to Agents and create a new Agent ("Override Test Agent"). | Agent creation form opens. Python Sandbox and Swarm Mode are ON, others OFF. |
| 13 | Disable Python Sandbox in this Agent (toggle OFF). | Python Sandbox switches to OFF for this Agent. |
| 14 | Enable Image Creation in this Agent (toggle ON). | Image Creation switches to ON for this Agent. |
| 15 | Save the Agent. | Agent saved successfully. |
| 16 | Navigate to Settings → General → Default Modules. | Default Modules section displayed. |
| 17 | Verify Agents project defaults are unchanged. | Python Sandbox and Swarm Mode are still ON. Image Creation is still OFF. |
| 18 | Create another new Agent ("Verify Defaults Agent"). | Agent creation form opens. |
| 19 | Verify modules match Agents project defaults. | Python Sandbox and Swarm Mode are ON, Image Creation is OFF. |

## Expected Final State

- "Override Test Chat" has custom modules (Image Creation OFF, Data Analysis ON, Planner ON)
- "Override Test Agent" has custom modules (Python Sandbox OFF, Swarm Mode ON, Image Creation ON)
- Project defaults remain unchanged
- New entities ("Verify Defaults Chat", "Verify Defaults Agent") use project defaults, not overrides from other entities

## Pass/Fail Criteria

**Pass:**
- User can override module states in individual Chat
- User can override module states in individual Agent
- Chat overrides do not modify project defaults
- Agent overrides do not modify project defaults
- New Chats use project Chats defaults (not affected by other Chats' overrides)
- New Agents use project Agents defaults (not affected by other Agents' overrides)

**Fail:**
- Changing module in Chat modifies project defaults
- Changing module in Agent modifies project defaults
- New entities inherit overrides from other entities instead of project defaults
