---
id: ELITEA-2643
title: "Default Modules Applied to New Chat"
priority: critical
type: functional
module: default-modules
status: ready
execution_type: manual
tags: [feat:settings, feat:modules, feat:Chats, eng:frontend, issue:6122, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6122]
---
# ELITEA-2643: Default Modules Applied to New Chats, Existing Chats Not Affected by Changes

**Module:** Default Modules · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that when a new Chat is created, the modules configured as enabled in project Default Modules settings are automatically pre-enabled in the new Chat. Existing Chats not affected by default Changes

**Coverage:**
- Enabled project defaults are applied to new Chats
- Disabled project defaults result in disabled modules in new Chats
- Module panel in new Chat reflects project defaults
- Module panel in existing Chat doesn't reflect project defaults

## Preconditions

- Logged into {{base_url}}
- User has permission to modify project settings and create Chats
- Browser: Chrome/Firefox/Edge (latest)

## Test Data

Project default configuration to set:
- Enable: Image Creation, Data Analysis, Planner
- Keep disabled: All other modules

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Settings → General → Default Modules. | Default Modules section is displayed. |
| 2 | Enable Image Creation toggle for Chats column. | Toggle switches to ON state. |
| 3 | Enable Data Analysis toggle for Chats column. | Toggle switches to ON state. |
| 4 | Enable Planner toggle for Chats column. | Toggle switches to ON state. |
| 5 | Ensure all other module toggles for Chats are OFF. | All other toggles are OFF. |
| 6 | Navigate to Chats from the sidebar. | Chats page is displayed. |
| 7 | Click "+Chat" or the button to create a new Chat. | New Chat creation flow starts. |
| 8 | Open the Modules panel in the new Chat (click + icon or Modules button). | Modules panel opens showing available modules. |
| 9 | Verify Image Creation module is enabled (ON). | Image Creation toggle is ON in the new Chat. |
| 10 | Verify Data Analysis module is enabled (ON). | Data Analysis toggle is ON in the new Chat. |
| 11 | Verify Planner module is enabled (ON). | Planner toggle is ON in the new Chat. |
| 12 | Verify all other modules are disabled (OFF). | All other toggles are OFF. |
| 13 | Open existing (old) Chat  | Existing Chat is openned. |
| 14 | Verify all modules are disabled (OFF). | All toggles are OFF (or according to this Chat specific configuration). |


## Expected Final State

New Chat has Image Creation, Data Analysis, and Planner modules enabled, all other modules disabled, matching the project default configuration.

## Pass/Fail Criteria

**Pass:**
- Modules enabled in project defaults are pre-enabled in new Chat
- Modules disabled in project defaults are pre-disabled in new Chat
- All module states in new Chat match project default configuration

**Fail:**
- Enabled project defaults are not applied to new Chat
- Disabled project defaults appear enabled in new Chat
- Module states in new Chat don't match project defaults
