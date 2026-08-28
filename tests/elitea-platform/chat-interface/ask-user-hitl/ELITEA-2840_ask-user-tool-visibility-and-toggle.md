---
id: ELITEA-2840
title: "ask_user - Tool visibility and toggle control in chat modules"
priority: critical
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [chat, hitl, internal-tools, ask-user, issue:6095]
requirements: [EliteaAI/elitea_issues#6095]
---

# ELITEA-2840: ask_user - Tool visibility and toggle control in chat modules

**Module:** Chat Interface · **Priority:** Critical · **Type:** Functional

**Objective:** Verify ask_user tool appears in internal tools list and can be toggled on/off for chat modules.

## Preconditions

- User is logged in to `{{base_url}}`
- User has access to internal tools settings
- Chat module is available

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/settings` |
| Tool name | ask_user |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Settings > Internal Tools or Chat Module Configuration | Settings page loads |
| 2 | Locate the ask_user tool in the internal tools list | ask_user tool is visible in the list |
| 3 | Verify the tool has a toggle control | Toggle switch is present next to ask_user tool |
| 4 | Enable the ask_user tool toggle | Toggle switches to ON state |
| 5 | Open a chat conversation | Chat interface loads with ask_user enabled |
| 6 | Navigate back to Settings > Internal Tools | Settings page loads |
| 7 | Disable the ask_user tool toggle | Toggle switches to OFF state |
| 8 | Open a new chat conversation | Chat interface loads with ask_user disabled |

## Expected Final State

ask_user tool is visible in internal tools list with working toggle control that persists across sessions.

## Pass/Fail Criteria

**Pass:** ask_user tool visible, toggle control works, state persists across navigation

**Fail:** Tool not visible, toggle non-functional, state does not persist
