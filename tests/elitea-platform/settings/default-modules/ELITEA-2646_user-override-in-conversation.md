---
id: ELITEA-2646
title: "User Override of Module State in Individual Chat"
priority: high
type: functional
module: default-modules
status: ready
execution_type: manual
tags: [feat:settings, feat:modules, feat:Chats, eng:frontend, issue:6122, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6122]
---
# ELITEA-2646: User Override of Module State in Individual Chat

**Module:** Default Modules · **Priority:** High · **Type:** Functional

**Objective:** Verify that users can override the project default module states in individual Chats — enabling modules that are disabled by default and disabling modules that are enabled by default.

**Coverage:**
- User can enable modules disabled by project defaults in a Chat
- User can disable modules enabled by project defaults in a Chat
- Override persists for that specific Chat
- Override does not affect project defaults or other Chats

## Preconditions

- Logged into {{base_url}}
- User has permission to modify project settings and Chat module settings
- Browser: Chrome/Firefox/Edge (latest)

## Test Data

Project default configuration:
- Enabled for Chats: Image Creation, Planner
- Disabled for Chats: All others (including Data Analysis, Python Sandbox)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Settings → General → Default Modules. | Default Modules section is displayed. |
| 2 | Configure defaults: Enable Image Creation and Planner for Chats, disable all others. | Configuration saved. |
| 3 | Navigate to Chats and create a new Chat ("Override Test Conv"). | Chat created. |
| 4 | Open Modules panel in the Chat. | Modules panel opens. Image Creation and Planner are ON, others OFF. |
| 5 | Disable Image Creation module in this Chat (toggle OFF). | Image Creation switches to OFF in this Chat. |
| 6 | Enable Data Analysis module in this Chat (toggle ON). | Data Analysis switches to ON in this Chat. |
| 7 | Enable Python Sandbox module in this Chat (toggle ON). | Python Sandbox switches to ON in this Chat. |
| 8 | Close the Modules panel. | Panel closes. |
| 9 | Refresh the page. | Page reloads. |
| 10 | Reopen Modules panel in "Override Test Conv". | Modules panel opens. |
| 11 | Verify overridden states persisted. | Image Creation is OFF, Data Analysis and Python Sandbox are ON, Planner is still ON. |
| 12 | Navigate to Settings → General → Default Modules. | Default Modules section displayed. |
| 13 | Verify project defaults are unchanged. | Image Creation and Planner are still ON by default. Data Analysis and Python Sandbox still OFF by default. |
| 14 | Create another new Chat ("Default Test Conv"). | Chat created. |
| 15 | Open Modules panel in new Chat. | Image Creation and Planner are ON (default), Data Analysis and Python Sandbox are OFF (default). |
| 16 | Return to "Override Test Conv" and verify overrides still in place. | Overrides persisted: Image Creation OFF, Data Analysis ON, Python Sandbox ON. |

## Expected Final State

- "Override Test Conv" has user-modified module states different from project defaults
- Project defaults remain unchanged
- New Chats continue to use project defaults
- Overrides persist across sessions

## Pass/Fail Criteria

**Pass:**
- User can enable default-disabled modules in individual Chat
- User can disable default-enabled modules in individual Chat
- Overrides persist after page refresh
- Overrides do not affect project defaults
- Other Chats continue to use project defaults

**Fail:**
- User cannot override module states in Chat
- Overrides do not persist
- Overrides modify project defaults
- Other Chats are affected by individual overrides
