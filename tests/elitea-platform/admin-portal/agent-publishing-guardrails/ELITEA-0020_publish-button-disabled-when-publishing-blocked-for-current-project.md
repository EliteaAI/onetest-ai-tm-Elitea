---
id: ELITEA-0020
title: "Publish Button Disabled When Publishing Blocked for Current Project"
priority: critical
type: functional
module: agent-publishing-guardrails
status: ready
execution_type: manual
tags: [feat:agent-publishing, guardrails, story:4434, r-2.0.2, publish, admin, p0]
requirements: [EliteaAI/elitea_issues#4434]
---
# ELITEA-0020: Publish Button Disabled When Publishing Blocked for Current Project

**Module:** Agent Publishing Guardrails · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that when the "Block Agent Publishing" guardrail is enabled without project exceptions (blocking all projects), the Publish action in Agent version actions menu is disabled and visually clear.

## Preconditions

Admin access to enable guardrail
At least one agent with a draft version ready to publish exists in a Team or Private project
elitea_core plugin can be reloaded

## Test Data

Agent: Any agent with draft version in Team or Private project
Project Type: Team or Private (not Public)
Guardrail: "Block Agent Publishing" enabled with NO exception projects

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Admin → Configuration → Guardrails | Guardrails page loads |
| 2 | Enable "Block Agent Publishing" toggle (set to ON) | Toggle switches to ON state, project exception dropdown appears |
| 3 | Leave project exception dropdown empty (no projects selected) | Dropdown shows no selected projects |
| 4 | Click "Save" button | Settings saved, "Reload required" indicator appears |
| 5 | Observe admin notification/toast message | Toast displays: "Changes saved. Plugin reload required to apply." |
| 6 | Reload the elitea_core plugin via Admin tools | Plugin reloads successfully |
| 7 | Navigate to the agent in a Team or Private project | Agent details page opens |
| 8 | Open the agent version details (draft version) | Version details panel shows |
| 9 | Locate the Version actions menu (three-dot menu or actions button) | Actions menu is accessible |
| 10 | Click on the Version actions menu to view available actions | Menu opens with list of actions |
| 11 | Locate the "Publish" action in the menu | "Publish" action is present in the menu |
| 12 | Observe the state of the "Publish" action | "Publish" action is disabled (greyed out, not clickable) |
| 13 | Verify disabled state is visually clear (greyed/dimmed styling) | Visual styling clearly indicates disabled state |
| 14 | Attempt to click the disabled "Publish" action | Click has no effect, action does not trigger |

## Expected Final State

Click has no effect, action does not trigger

## Pass/Fail Criteria

PASS:
- Guardrail can be enabled and saved successfully
- "Reload required" indicator appears after save
- Admin notification toast appears with correct message
- After plugin reload, "Publish" action is disabled in Agent version menu
- Disabled state is visually clear (greyed out, not clickable)
- Clicking disabled "Publish" has no effect

FAIL:
- Guardrail cannot be enabled or saved
- No "Reload required" indicator or notification appears
- "Publish" action remains enabled after plugin reload
- Disabled state is not visually clear
- "Publish" can still be clicked despite being disabled
