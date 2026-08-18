---
id: ELITEA-2645
title: "Multiple Modules Enabled Simultaneously"
priority: high
type: functional
module: default-modules
status: ready
execution_type: manual
tags: [feat:settings, feat:modules, feat:Chats, feat:agents, eng:frontend, issue:6122, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6122]
---
# ELITEA-2645: Multiple Modules Enabled Simultaneously

**Module:** Default Modules · **Priority:** High · **Type:** Functional

**Objective:** Verify that multiple modules can be enabled simultaneously and all enabled modules are correctly applied to new Chats and Agents.

**Coverage:**
- Multiple modules can be enabled at once
- All enabled modules are applied to new Chats
- All enabled modules are applied to new Agents
- System handles maximum configuration (all 10 modules enabled)

## Preconditions

- Logged into {{base_url}}
- User has permission to modify project settings and create Chats/Agents
- All module toggles start in OFF state
- Browser: Chrome/Firefox/Edge (latest)

## Test Data

Test configuration 1 (partial):
- Enable for Chats: Image Creation, Data Analysis, Planner
- Enable for Agents: Python Sandbox, Swarm Mode, Smart Tools Selection

Test configuration 2 (all modules):
- Enable all 10 modules for both Chats and Agents

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Settings → General → Default Modules. | Default Modules section is displayed. |
| 2 | Enable Image Creation, Data Analysis, Planner for Chats column. | Three toggles switch to ON. |
| 3 | Enable Python Sandbox, Swarm Mode, Smart Tools Selection for Agents column. | Three toggles switch to ON. |
| 4 | Refresh the page. | Page reloads. |
| 5 | Verify all 6 enabled toggles are still ON. | All configured toggles persisted. |
| 6 | Create a new Chat. | Chat created. |
| 7 | Open Modules panel and verify enabled modules. | Image Creation, Data Analysis, Planner are ON. Others are OFF. |
| 8 | Create a new Agent. | Agent creation form opens. |
| 9 | Verify enabled modules in Agent config. | Python Sandbox, Swarm Mode, Smart Tools Selection are ON. Others are OFF. |
| 10 | Return to Default Modules and enable ALL modules for Chats. | All 10 Chats column toggles are ON. |
| 11 | Enable ALL modules for Agents column. | All 10 Agents column toggles are ON. |
| 12 | Refresh the page. | Page reloads without errors. |
| 13 | Verify all 20 toggles (10 × 2 columns) are ON. | All toggles persisted in ON state. |
| 14 | Create a new Chat. | Chat created without errors. |
| 15 | Verify all 10 modules are enabled in the new Chat. | All modules are ON in new Chat. |
| 16 | Create a new Agent. | Agent creation form opens without errors. |
| 17 | Verify all 10 modules are enabled in the new Agent. | All modules are ON in new Agent. |
| 18 | Save and test the Agent (send a message). | Agent works correctly with all modules enabled. |

## Expected Final State

System handles multiple modules enabled simultaneously, including the maximum configuration of all 10 modules for both entity types.

## Pass/Fail Criteria

**Pass:**
- Multiple modules can be enabled simultaneously without errors
- All enabled modules are correctly applied to new Chats
- All enabled modules are correctly applied to new Agents
- System handles all 10 modules enabled without performance issues
- New entities function correctly with multiple modules enabled

**Fail:**
- Enabling multiple modules causes errors
- Some enabled modules are missing in new entities
- System errors when all modules are enabled
- Performance degradation with many modules enabled
