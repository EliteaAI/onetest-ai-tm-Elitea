---
id: ELITEA-0012
title: "Guardrail Blocks Publishing in All Projects When No Exceptions Selected"
priority: medium
type: functional
module: agent-publishing-guardrails
status: ready
execution_type: manual
tags: [feat:agent-publishing, global-block, guardrails, story:4434, r-2.0.2, admin, p2]
requirements: [EliteaAI/elitea_issues#4434]
---
# ELITEA-0012: Guardrail Blocks Publishing in All Projects When No Exceptions Selected

**Module:** Agent Publishing Guardrails · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that when "Block Agent Publishing" guardrail is enabled with NO exception projects selected, the Publish action is disabled in ALL Team and Private projects.

## Preconditions

Admin access to configure guardrail
At least 2 Team projects and 2 Private projects with agents
elitea_core plugin can be reloaded

## Test Data

Toggle: ON
Exception projects: NONE (empty selection)
Test projects: Team Project 1, Team Project 2, Private Project 1, Private Project 2

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Admin → Configuration → Guardrails | Guardrails page loads |
| 2 | Enable "Block Agent Publishing" toggle (ON) | Toggle ON, dropdown appears |
| 3 | Leave exception projects dropdown EMPTY (select no projects) | Dropdown shows no selected projects |
| 4 | Click "Save" | Settings saved |
| 5 | Reload the elitea_core plugin | Plugin reloads successfully |
| 6 | Navigate to an agent in Team Project 1 | Agent details page opens |
| 7 | Open Version actions menu and check "Publish" action state | "Publish" is DISABLED (greyed out) |
| 8 | Navigate to an agent in Team Project 2 | Agent details page opens |
| 9 | Check "Publish" action state | "Publish" is DISABLED |
| 10 | Navigate to an agent in Private Project 1 | Agent details page opens |
| 11 | Check "Publish" action state | "Publish" is DISABLED |
| 12 | Navigate to an agent in Private Project 2 | Agent details page opens |
| 13 | Check "Publish" action state | "Publish" is DISABLED |
| 14 | Verify "Publish" action cannot be triggered in any project | Clicking disabled "Publish" has no effect in all tested projects |

## Expected Final State

Clicking disabled "Publish" has no effect in all tested projects

## Pass/Fail Criteria

PASS:
- "Publish" action is disabled in ALL Team projects
- "Publish" action is disabled in ALL Private projects
- Visual disabled state is consistent across all projects
- No project allows publishing when no exceptions are configured

FAIL:
- "Publish" is enabled in any Team or Private project
- Disabled state is inconsistent across projects
- Any project allows publishing despite guardrail being active with no exceptions
