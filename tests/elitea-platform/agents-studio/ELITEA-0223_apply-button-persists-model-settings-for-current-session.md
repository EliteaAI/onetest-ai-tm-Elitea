---
id: ELITEA-0223
title: "Apply Button Persists Model Settings for Current Session"
priority: high
type: functional
module: agents-studio
status: draft
execution_type: manual
tags: [feat: agent-publishing, meta:needs_refinement, r-2.0.3, 4644]
requirements: [EliteaAI/elitea_issues#4644]
---
# ELITEA-0223: Apply Button Persists Model Settings for Current Session

**Module:** Agents Studio · **Priority:** High · **Type:** Functional

**Objective:** Verify that clicking Apply in the Model Settings dialog saves all changed settings and they are still reflected when the dialog is reopened within the same session.

**Coverage:**
- All changed settings (Creativity + Max Tokens) are persisted after Apply
- Values visible on dialog reopen

## Preconditions

- Published agent is open in chat, Model Settings dialog is accessible

## Test Data

Creativity: 3, Max Completion Tokens: Custom 1024

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Model Settings dialog. | Dialog visible. |
| 2 | Set Creativity to 3 and Max Tokens to Custom 1024. | Values set. |
| 3 | Click Apply. | Dialog closes. |
| 4 | Reopen Model Settings dialog without refreshing the page. | Dialog shows Creativity 3 and Max Tokens 1024. |

## Expected Final State

Dialog shows Creativity 3 and Max Tokens 1024.

## Pass/Fail Criteria

**Pass:**
- Both Creativity and Max Tokens values are retained after Apply
- Reopen shows exact values that were applied

**Fail:**
- Values reset to defaults after Apply
- Only one of the two values is persisted
