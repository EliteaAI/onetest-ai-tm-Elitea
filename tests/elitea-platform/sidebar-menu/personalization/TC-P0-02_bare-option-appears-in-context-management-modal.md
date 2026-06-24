---
id: TC-P0-02
title: "Verify Bare Option Appears in Context Management Modal"
priority: critical
type: functional
module: sidebar-menu/personalization
status: ready
execution_type: manual
tags: [p0, bare-personality, context-management, r-2.0.4, 5264]
requirements: [EliteaAI/elitea_issues#5264]
---
# TC-P0-02: Verify Bare Option Appears in Context Management Modal

**Module:** Personalization · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the "Bare" personality option appears in the Context Management modal persona dropdown and is accessible during active conversations.

**Coverage:**
- "Bare" option visible in Context Management modal
- USER INSTRUCTIONS section displays persona dropdown correctly
- "Bare" appears alongside other personalities
- Option is selectable from within conversation context

## Preconditions

- User is logged into EliteaUI
- User has started a conversation (or can start one)
- Context Management modal is accessible
- "Bare" personality has been added to the system

## Test Data

- User: Valid test user account
- Conversation: Any active conversation
- Expected personas: Generic, QA, Nerdy, Quirky, Cynical, None, Bare

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Chat interface. | Chat interface loads successfully. |
| 2 | Start a new conversation or open an existing one. | Conversation is active. |
| 3 | Locate and click the "Context Management" button/icon in the conversation header. | Context Management modal opens. |
| 4 | Scroll down to the "USER INSTRUCTIONS" section. | USER INSTRUCTIONS section is visible. |
| 5 | Locate the "Default Persona" or persona dropdown. | Persona dropdown is present. |
| 6 | Click on the dropdown to expand the list. | Dropdown expands showing all options. |
| 7 | Scroll through all available options. | All personality options are listed. |
| 8 | Verify "Bare" option is visible in the dropdown list. | "Bare" option appears in the list. |
| 9 | Verify "Bare" appears alongside: Generic, QA, Nerdy, Quirky, Cynical, None. | All expected options including "Bare" are present. |
| 10 | Check that "Bare" is selectable (not disabled). | "Bare" option is interactive and can be selected. |

## Expected Final State

Context Management modal displays "Bare" personality option in the persona dropdown, accessible and selectable during conversations.

## Pass/Fail Criteria

**Pass:**
- Context Management modal opens without errors
- USER INSTRUCTIONS section is visible
- Persona dropdown contains "Bare" option
- "Bare" is selectable and not disabled
- Dropdown renders correctly

**Fail:**
- Context Management modal fails to open
- "Bare" option is missing from dropdown
- Option is disabled or grayed out
- UI rendering issues present
