---
id: ELITEA-0222
title: "Max Completion Tokens — Default Mode Accepted in Model Settings"
priority: high
type: functional
module: agents-studio
status: draft
execution_type: manual
tags: [feat: agent-publishing, meta:needs_refinement, r-2.0.3, 4644]
requirements: [EliteaAI/elitea_issues#4644]
---
# ELITEA-0222: Max Completion Tokens — Default Mode Accepted in Model Settings

**Module:** Agents Studio · **Priority:** High · **Type:** Functional

**Objective:** Verify that selecting "Default" for Max Completion Tokens in Model Settings is accepted and applied without error.

**Coverage:**
- Default radio button is selectable
- Max Tokens input is hidden/disabled when Default is selected

## Preconditions

- Model Settings dialog is open for a published agent chat session

## Test Data

Radio button: Default

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Model Settings dialog. | Dialog shows Max Completion Tokens section with Default/Custom radio buttons. |
| 2 | Select the Default radio button. | Default is selected; Max Tokens field becomes hidden or disabled. |
| 3 | Click Apply. | Dialog closes without error. |
| 4 | Reopen Model Settings. | Default radio button is still selected. |

## Expected Final State

Default radio button is still selected.

## Pass/Fail Criteria

**Pass:**
- Default radio button is selectable
- Max Tokens field is hidden/disabled in Default mode
- Setting is retained after Apply

**Fail:**
- Default cannot be selected, or selecting it causes an error
- Max Tokens field remains visible/editable in Default mode
