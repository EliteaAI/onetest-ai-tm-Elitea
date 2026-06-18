---
id: ELITEA-0013
title: "Disabling Guardrail Re-enables Publishing Globally"
priority: medium
type: functional
module: agent-publishing-guardrails
status: ready
execution_type: manual
tags: [feat:agent-publishing, guardrails, story:4434, disable, r-2.0.2, admin, p2]
requirements: [EliteaAI/elitea_issues#4434]
---
# ELITEA-0013: Disabling Guardrail Re-enables Publishing Globally

**Module:** Agent Publishing Guardrails · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that after "Block Agent Publishing" guardrail has been enabled and enforced, disabling the guardrail (toggle OFF), saving, and reloading the plugin re-enables the Publish action in ALL projects.

## Preconditions

"Block Agent Publishing" guardrail is currently enabled (toggle ON)
Guardrail is enforced (Publish action is disabled in at least one project)
elitea_core plugin can be reloaded

## Test Data

Initial state: Guardrail ON, Publish disabled globally
Target state: Guardrail OFF, Publish enabled globally

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Verify current state: Navigate to an agent in a non-exception project | Agent details page opens |
| 2 | Check "Publish" action state | "Publish" is DISABLED (guardrail is active) |
| 3 | Navigate to Admin → Configuration → Guardrails | Guardrails page loads |
| 4 | Verify "Block Agent Publishing" toggle is ON | Toggle is ON |
| 5 | Click the toggle to switch it to OFF | Toggle switches to OFF, exception dropdown disappears |
| 6 | Click "Save" button | Settings saved, "Reload required" indicator appears |
| 7 | Reload the elitea_core plugin | Plugin reloads successfully |
| 8 | Navigate to an agent in a Team project | Agent details page opens |
| 9 | Open Version actions menu and check "Publish" action | "Publish" is ENABLED (clickable, not greyed out) |
| 10 | Navigate to an agent in a different Private project | Agent details page opens |
| 11 | Check "Publish" action state | "Publish" is ENABLED |
| 12 | Navigate to an agent in another Team project | Agent details page opens |
| 13 | Check "Publish" action state | "Publish" is ENABLED |
| 14 | Verify "Publish" action is now enabled in ALL Team and Private projects | All projects have enabled "Publish" action |

## Expected Final State

All projects have enabled "Publish" action

## Pass/Fail Criteria

PASS:
- Toggle can be switched from ON to OFF successfully
- Exception dropdown disappears when toggle is OFF
- After save and plugin reload, "Publish" action is enabled in ALL Team and Private projects
- No projects have disabled "Publish" action after guardrail is turned OFF

FAIL:
- Toggle cannot be switched to OFF or does not save
- Exception dropdown remains visible when toggle is OFF
- "Publish" action remains disabled in any project after guardrail is disabled
- Guardrail continues to be enforced despite being turned OFF and plugin reloaded
