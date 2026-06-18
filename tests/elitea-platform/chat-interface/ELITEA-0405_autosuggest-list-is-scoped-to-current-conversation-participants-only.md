---
id: ELITEA-0405
title: "`/` Autosuggest List Is Scoped to Current Conversation Participants Only"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [user_story:2925, feat:chat, r-2.0.3]
requirements: [EliteaAI/elitea_issues#2925]
---
# ELITEA-0405: `/` Autosuggest List Is Scoped to Current Conversation Participants Only

**Module:** Chat Interface · **Priority:** High · **Type:** Functional

**Objective:** Verify the `/` autosuggest shows only Toolkits/MCPs added to the current conversation Participants, not all project-level toolkits.

**Coverage:**
- Added toolkits appear in dropdown
- Non-added project toolkits are absent from dropdown
- Non-toolkit participant types (agents, pipelines) are absent

## Preconditions

- Logged in; at least three toolkits exist in the project: Artifacts, Jira Integration, github
- New conversation created with Artifacts and Jira Integration added to Participants; github NOT added

## Test Data

- Participants: Artifacts, Jira Integration
- Non-participant toolkit: github

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open new chat conversation. Add Artifacts and Jira Integration toolkits to Participants. | Both appear under Toolkits in the Participants panel. |
| 2 | Click the chat input and type /. | Autosuggest dropdown opens. |
| 3 | Inspect all items listed in the dropdown. | Artifacts and Jira Integration are present. |
| 4 | Verify github toolkit is NOT in the list. | github does not appear. |
| 5 | Verify no agent or pipeline entries appear. | Only Toolkit/MCP entries are listed. |

## Expected Final State

Only Toolkit/MCP entries are listed.

## Pass/Fail Criteria

**Pass:**
- Dropdown lists exactly Artifacts and Jira Integration (and any added MCPs)
- github (non-participant) is absent

**Fail:**
- Project-level toolkits not in Participants appear in the dropdown
- Agent/pipeline entries appear
