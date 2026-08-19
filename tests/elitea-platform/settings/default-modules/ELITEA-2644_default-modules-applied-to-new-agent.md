---
id: ELITEA-2644
title: "Default Modules Applied to New Agent"
priority: critical
type: functional
module: default-modules
status: ready
execution_type: manual
tags: [feat:settings, feat:modules, feat:agents, eng:frontend, issue:6122, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6122]
---
# ELITEA-2644: Default Modules Applied to New Agent. Existing Agents Not Affected by Default Changes

**Module:** Default Modules · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that when a new Agent is created, the modules configured as enabled in project Default Modules settings (Agents column) are automatically pre-enabled in the new Agent. Existing Agents not affected by default changes

**Coverage:**
- Enabled project defaults (Agents column) are applied to new Agents
- Disabled project defaults result in disabled modules in new Agents
- Module configuration in new Agent reflects project defaults
- Module configuration in existing Agent doesn't reflect project defaults

## Preconditions

- Logged into {{base_url}}
- User has permission to modify project settings and create Agents
- Browser: Chrome/Firefox/Edge (latest)

## Test Data

Project default configuration to set (Agents column):
- Enable: Image Creation, Python Sandbox, Swarm Mode
- Keep disabled: All other modules

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Settings → General → Default Modules. | Default Modules section is displayed. |
| 2 | Enable Image Creation toggle for Agents column. | Toggle switches to ON state. |
| 3 | Enable Python Sandbox toggle for Agents column. | Toggle switches to ON state. |
| 4 | Enable Swarm Mode toggle for Agents column. | Toggle switches to ON state. |
| 5 | Ensure all other module toggles for Agents column are OFF. | All other toggles are OFF. |
| 6 | Navigate to Agents from the sidebar. | Agents page is displayed. |
| 7 | Click "+Agent" to create a new Agent. | New Agent creation form opens. |
| 8 | Fill in required Agent details (name, system prompt, etc.). | Agent details are entered. |
| 9 | Locate the Modules configuration section in the Agent form. | Modules section is visible with toggle switches. |
| 10 | Verify Image Creation module is enabled (ON). | Image Creation toggle is ON in the new Agent. |
| 11 | Verify Python Sandbox module is enabled (ON). | Python Sandbox toggle is ON in the new Agent. |
| 12 | Verify Swarm Mode module is enabled (ON). | Swarm Mode toggle is ON in the new Agent. |
| 13 | Verify all other modules are disabled (OFF). | All other toggles are OFF. |
| 14 | Open existing (old) Agent. | Existing Agent is openned. |
| 15 | Verify all modules are disabled (OFF). | All toggles are OFF (or according to this Agent specific configuration). |


## Expected Final State

New Agent has Image Creation, Python Sandbox, and Swarm Mode modules enabled, all other modules disabled, matching the project default configuration for Agents.

## Pass/Fail Criteria

**Pass:**
- Modules enabled in project defaults (Agents column) are pre-enabled in new Agent
- Modules disabled in project defaults are pre-disabled in new Agent
- All module states in new Agent match project default configuration

**Fail:**
- Enabled project defaults are not applied to new Agent
- Disabled project defaults appear enabled in new Agent
- Module states in new Agent don't match project defaults (Agents column)
