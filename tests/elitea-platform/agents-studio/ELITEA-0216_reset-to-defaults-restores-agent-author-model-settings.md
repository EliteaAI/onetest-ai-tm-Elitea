---
id: ELITEA-0216
title: "Reset to Defaults Restores Agent-Author Model Settings"
priority: high
type: functional
module: agents-studio
status: draft
execution_type: manual
tags: [feat: agent-publishing, meta:needs_refinement, r-2.0.3, 4644]
requirements: [EliteaAI/elitea_issues#4644]
---
# ELITEA-0216: Reset to Defaults Restores Agent-Author Model Settings

**Module:** Agents Studio · **Priority:** High · **Type:** Functional

**Objective:** Verify that clicking "Reset to defaults" in the Model Settings dialog reverts all settings to the agent author's original configuration.

**Coverage:**
- Reset to defaults restores Creativity and Max Completion Tokens to original values

## Preconditions

- Known default values for the agent (e.g. Creativity = 1, Max Tokens = Custom 2048)
- User has changed settings (Creativity = 4, Max Tokens = Auto)

## Test Data

Author default: Creativity 1, Max Tokens Custom 2048
User changes: Creativity 4, Auto

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Model Settings, change Creativity to 4 and set Max Tokens to Auto. Click Apply. | Settings applied. |
| 2 | Reopen Model Settings. | Creativity = 4, Auto selected. |
| 3 | Click Reset to defaults. | Values revert to Creativity = 1, Max Tokens = Custom 2048 (author's config). |
| 4 | Click Apply. | Defaults confirmed. |
| 5 | Reopen dialog. | Shows default values. |

## Expected Final State

Shows default values.

## Pass/Fail Criteria

**Pass:**
- Reset reverts all values to the agent author's original defaults
- Reopen after reset + Apply shows the correct default values

**Fail:**
- Reset button has no effect
- Defaults shown after reset do not match the agent author's configured values
