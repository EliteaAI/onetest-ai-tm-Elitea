---
id: ELITEA-4785
title: "Existing agent with saved modules shows the correct switch states in the Modules dropdown"
priority: critical
type: functional
module: agents
status: ready
execution_type: manual
tags: [feat:agents, nfr:ui, modules, 7380]
requirements: [EliteaAI/elitea_issues#7380]
---
# ELITEA-4785: Existing agent with saved modules shows the correct switch states in the Modules dropdown

**Module:** Agents · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that for Agents with module configuration saved before or after the dropdown change, the "+ Modules" dropdown loads and displays the correct ON/OFF state for every module.

**Coverage:**
- Agent with several modules enabled
- Agent with no modules enabled
- Agent created before the UI change (migration of existing configuration)

## Preconditions

- Logged in to {{base_url}}
- Agent A: existing Agent with several modules ON (preferably configured before the dropdown was introduced)
- Agent B: existing Agent with all modules OFF
- Known saved module states for both Agents (e.g. noted from the Agent configuration or a previous run)
- Browser: Chrome (latest)

## Test Data

Agent A, Agent B

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Agent A and click "+ Modules" | Dropdown opens |
| 2 | Compare every module switch with the known saved states (scroll to see all modules) | Each enabled module is ON, each other module is OFF |
| 3 | Check that Save and Discard are disabled | No unsaved changes are reported just from opening the dropdown |
| 4 | Open Agent B and click "+ Modules" | All module switches are OFF |
| 5 | Chat with Agent A and use a feature of one enabled module (e.g. attach a file if Attachments is ON) | The enabled module works in chat, confirming the displayed state matches the real configuration |

## Expected Final State

The dropdown reflects the saved module configuration of each Agent.

## Pass/Fail Criteria

**Pass:** All module switches match the saved configuration and no false unsaved changes appear
**Fail:** Any switch shows a wrong state, or opening the dropdown marks the Agent as changed
