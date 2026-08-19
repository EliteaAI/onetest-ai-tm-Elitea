---
id: ELITEA-2652
title: "Default Modules Applied to New Chats and Agents, Existing Not Affected"
priority: critical
type: functional
module: default-modules
status: draft
execution_type: manual
tags: [feat:settings, feat:modules, feat:chats, feat:agents, eng:frontend, eng:automation, issue:6122, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6122]
---
# ELITEA-2652: Default Modules Applied to New Chats and Agents, Existing Not Affected

**Module:** Default Modules · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that project default module settings are applied to newly created Chats and Agents, and that existing Chats/Agents are not affected when defaults change.

**Coverage:**
- Enabled project defaults applied to new Chats
- Enabled project defaults applied to new Agents
- Existing Chats not affected by default changes
- Existing Agents not affected by default changes

## Preconditions

- Logged into {{base_url}}
- User has permission to modify project settings and create Chats/Agents
- One existing Chat available (created before test)
- One existing Agent available (created before test)
- Browser: Chrome/Firefox/Edge (latest)

## Test Data

Project default configuration:
- For Chats: Enable Image Creation, Data Analysis, Planner
- For Agents: Enable Image Creation, Python Sandbox, Swarm Mode

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Settings → General → Default Modules. | Default Modules section is displayed. |
| 2 | Enable Image Creation, Data Analysis, Planner toggles for Chats column. | Three toggles switch to ON. |
| 3 | Enable Image Creation, Python Sandbox, Swarm Mode toggles for Agents column. | Three toggles switch to ON. |
| 4 | Navigate to Chats and create a new Chat. | New Chat created. |
| 5 | Open the Modules panel in the new Chat. | Modules panel opens. |
| 6 | Verify Image Creation, Data Analysis, Planner are enabled (ON). | Three modules are ON in the new Chat. |
| 7 | Verify all other modules are disabled (OFF). | All other toggles are OFF. |
| 8 | Open an existing Chat (created before this test). | Existing Chat opens. |
| 9 | Open the Modules panel in the existing Chat. | Modules panel opens. |
| 10 | Verify modules in existing Chat are NOT affected by new defaults. | Modules remain as they were configured before (likely all OFF or per previous config). |
| 11 | Navigate to Agents and create a new Agent. | New Agent creation form opens. |
| 12 | Locate the Modules configuration section. | Modules section is visible. |
| 13 | Verify Image Creation, Python Sandbox, Swarm Mode are enabled (ON). | Three modules are ON in the new Agent. |
| 14 | Verify all other modules are disabled (OFF). | All other toggles are OFF. |
| 15 | Open an existing Agent (created before this test). | Existing Agent opens for editing. |
| 16 | Verify modules in existing Agent are NOT affected by new defaults. | Modules remain as they were configured before. |

## Expected Final State

- New Chat has Image Creation, Data Analysis, Planner enabled (from Chats defaults)
- New Agent has Image Creation, Python Sandbox, Swarm Mode enabled (from Agents defaults)
- Existing Chat and Agent retain their original module configuration

## Pass/Fail Criteria

**Pass:**
- New Chat has correct modules enabled from project Chats defaults
- New Agent has correct modules enabled from project Agents defaults
- Existing Chat modules not affected by default changes
- Existing Agent modules not affected by default changes

**Fail:**
- New Chat missing enabled modules or has wrong modules enabled
- New Agent missing enabled modules or has wrong modules enabled
- Existing Chat modules changed to match new defaults
- Existing Agent modules changed to match new defaults
