---
id: ELITEA-0065
title: "Save Button Persists Configuration on Newly Created Agent"
priority: critical
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4967]
---
# ELITEA-0065: Save Button Persists Configuration on Newly Created Agent

**Module:** Agents · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that clicking the Save button on a newly created agent (after its initial creation) persists all configuration changes and suppresses the unsaved-changes navigation warning.

**Coverage:**
- Save button is functional immediately after the agent is first created and saved
- Configuration changes (e.g., updated Instructions) are persisted after clicking Save
- No unsaved-changes modal appears when navigating away after a successful save
- Page reflects the saved state with no pending-changes indicator

## Preconditions

- Logged in to {{base_url}}
- User has permission to create agents in the active project

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Agents in the main menu → click + New Agent → fill in Name and Description → click Save | Agent is created and the agent configuration page loads |
| 2 | Make a change to the agent configuration (e.g., update the Instructions field with a distinct test string) | The Instructions field reflects the change; an unsaved-state indicator or dirty flag is visible |
| 3 | Click the Save button | Save action completes — the page refreshes or shows a success indicator; no error is displayed; no silent no-op |
| 4 | Navigate away from the agent (e.g., click another section in the sidebar) | No "There are unsaved changes. Are you sure you want to leave?" modal appears |
| 5 | Return to the agent configuration page | The Instructions field retains the value entered in step 2 |

## Expected Final State

The Instructions field retains the value entered in step 2

## Pass/Fail Criteria

**Pass:**
- Save button triggers a save action (page refresh or success notification)
- Configuration change is persisted; visible on return
- Unsaved-changes modal does NOT appear when navigating away after saving

**Fail:**
- Save button does nothing (no feedback, no refresh, no notification)
- Unsaved-changes modal appears despite having clicked Save
- Configuration changes are lost after navigating away and returning
