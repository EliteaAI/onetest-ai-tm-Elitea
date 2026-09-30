---
id: ELITEA-3444
title: "Chat Templates: Create, Rename, Delete, and Default Selection"
priority: high
type: functional
module: settings-chat-configuration
status: draft
execution_type: manual
tags: [feat:settings, feat:chat-config, story:6724, regression]
requirements: [EliteaAI/elitea_issues#6724]
---
# ELITEA-3444: Chat Templates: Create, Rename, Delete, and Default Selection

**Module:** Settings → General → Chat Configuration · **Priority:** High · **Type:** Functional

**Objective:** Verify core template CRUD operations and default selection behavior — regression checks for #6799 (first template should not auto-become default) and foundational acceptance criteria.

**Coverage:** [EliteaAI/elitea_issues#6724](https://github.com/EliteaAI/elitea_issues/issues/6724) enhancement acceptance.

## Preconditions

- User is logged in as an Admin to a project
- Chat Configuration section is accessible in Settings → General

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Settings → General → Chat Configuration. | Chat Configuration section displays with Chat templates block, counter, and "New template" button. |
| 2 | Click **+ New template**. | A new template named `Template 1` is created, selected, and the name field is focused and text selected. |
| 3 | Verify template is **not** marked as default (no "Default" badge). | No badge present; template is created without auto-default status (regression check for **#6799**). |
| 4 | Rename the template to "Team Brainstorm". Save. | Template name updates to "Team Brainstorm"; counter shows `1 of 5`. |
| 5 | Create a second template named "Code Review". Save. | Counter shows `2 of 5`; second template is selectable; neither is marked as default. |
| 6 | Select the second template and click **Set as default**. | "Set as default" button is visible on the first template; "Team Brainstorm" now shows the **"Default"** badge; button disappears from "Team Brainstorm" row. |
| 7 | Select "Team Brainstorm". | Template editor loads with "Team Brainstorm" data; **"Set as default"** button is visible because it's not the default. |
| 8 | Delete "Team Brainstorm" by clicking the delete icon. Confirm the dialog. | Template is removed; counter shows `1 of 5`; "Code Review" (the default) remains and is selected. |
| 9 | Try to delete "Code Review". | **Delete button is hidden** because it's the default template; deletion is blocked. |

## Expected Final State

- Templates can be created (unnamed defaults to `Template N`), renamed (with validation), and deleted (unless they are the default).
- Only one template is marked as default at any time; "Set as default" button is visible only for non-default templates.
- First-created template does **not** automatically become the default (regression check for #6799).

## Pass/Fail Criteria

**Pass:**
- All steps complete as expected
- No auto-default on first template creation (regression: #6799)
- Counter and badges update correctly
- Delete button hidden/shown correctly

**Fail:**
- First template auto-becomes default (regression of #6799)
- Multiple templates marked as default simultaneously
- Delete succeeds on default template
- Delete button behavior inconsistent
