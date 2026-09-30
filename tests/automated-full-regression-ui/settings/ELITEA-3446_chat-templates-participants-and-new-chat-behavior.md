---
id: ELITEA-3446
title: "Chat Templates: Preconfigured Participants and New Chat Population"
priority: high
type: functional
module: settings-chat-configuration
status: draft
execution_type: manual
tags: [feat:settings, feat:chat, feat:chat-config, story:6724, story:6358]
requirements: [EliteaAI/elitea_issues#6724, EliteaAI/elitea_issues#6358]
---
# ELITEA-3446: Chat Templates: Preconfigured Participants and New Chat Population

**Module:** Settings → Chat Configuration & Chat UI · **Priority:** High · **Type:** Functional

**Objective:** Verify preconfigured participants are correctly added to templates, new chats inherit the default template's participants, and the single-participant rule (one configured = becomes active) works end-to-end.

**Coverage:** [EliteaAI/elitea_issues#6724](https://github.com/EliteaAI/elitea_issues/issues/6724) + [#6358](https://github.com/EliteaAI/elitea_issues/issues/6358) (foundation).

## Preconditions

- User is logged in as an Admin to a project with existing agents, pipelines, toolkits, MCPs
- Chat Configuration section is accessible in Settings → General

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Chat Configuration and select the default template (or create one named "Default"). | Template editor opens with "Pre-configured participants" section visible and empty. |
| 2 | In the participant picker, select **Agents** chip and search for an agent. Add **one agent**. Save. | Agent pill appears in the selected list; **Save** enables. Save succeeds; agent persists. |
| 3 | Open the chat UI and click **+ Chat** to create a new chat. | New chat opens with the agent **already added as a participant** and as the **active participant** (cursor ready to send message to it, per the single-participant rule from #6358). |
| 4 | Go back to Chat Configuration, select the same template, and add **one pipeline** to the participant list. Save. | Participants now shows: agent + pipeline (2 participants). Save succeeds. |
| 5 | Create another new chat. | Both agent and pipeline are pre-populated; **neither is active** (because more than one participant exists, the single-participant rule does not apply). |
| 6 | In Chat Configuration, delete the agent from the template. Add a **toolkit** and an **MCP**. Save. | Participant list now shows: pipeline, toolkit, MCP (3 total, agent removed). |
| 7 | Create another new chat. | Participants populated: pipeline, toolkit, MCP; none is active (count > 1). Existing chats created before step 6 are **unaffected** (they still have agent + pipeline). |
| 8 | (Team projects only) Verify **Users** chip is available. Add a teammate. (Private projects only) Verify **Users** chip is **not rendered**. | Team: Users chip visible and searchable; teammate added. Private: Users chip absent from chips list. |

## Expected Final State

- Preconfigured participants correctly persist in templates.
- New chats inherit the **default template's** participant list (not other templates).
- Single-participant rule works: exactly one = active; zero or 2+ = none active.
- Editing a template's participants does **not** affect existing chats (only new chats use the updated list).
- Users participant type is visible in Team projects, absent in Private.

## Pass/Fail Criteria

**Pass:**
- Steps 3 and 5: new chats correctly inherit default template participants
- Step 3: single agent is active participant
- Step 5: multiple participants, none active
- Step 7: existing chats unaffected after template edit
- Team/Private: Users chip renders/absent correctly

**Fail:**
- New chats do not inherit default template participants
- Single-participant rule fails
- Editing template affects existing chats
- Users chip present in Private project
