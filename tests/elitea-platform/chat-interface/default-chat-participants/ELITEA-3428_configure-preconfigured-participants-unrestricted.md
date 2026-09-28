---
id: ELITEA-3428
title: "Admins Can Configure Any Agents and Pipelines as Preconfigured Chat Participants"
priority: medium
type: functional
module: chat
status: draft
execution_type: manual
tags: [feat:chat, feat:project-setup, story:6358, default-chat-config, settings]
requirements: [EliteaAI/elitea_issues#6358]
---
# ELITEA-3428: Admins Can Configure Any Agents and Pipelines as Preconfigured Chat Participants

**Module:** Chat · **Priority:** Medium · **Type:** Functional

**Objective:** Confirm an admin can open Project Settings → "Default Chat Configuration" → "Pre-configured participants", add agents and/or pipelines without restriction on type or count, edit the list (remove one, add another), and have the saved list actually used as the participant set for new chats.

**Coverage:** AC — the shipped Settings UI section (confirmed live) backing `chat_config.participants` via `elitea_core#455`.

## Preconditions

- Logged in as a project **admin**
- The project has at least 3 agents and 2 pipelines available to select from

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Project Settings → "Default Chat Configuration" → "Pre-configured participants". | Section is visible and the participant picker is usable. |
| 2 | Add one agent as a preconfigured participant and Save. | Save succeeds; reloading the settings page still shows the agent. |
| 3 | Add one pipeline as a preconfigured participant and Save. | Save succeeds; both the agent and pipeline are listed together, no type restriction is enforced. |
| 4 | Add two more agents/pipelines (mixed types) and Save. | All are accepted — no artificial cap on count. |
| 5 | Remove one previously-added participant, add a different one instead, and Save. | The edited set persists; the removed one is gone and the new one is present after reload. |
| 6 | Open a brand-new chat. | The participant panel reflects exactly the current saved list from step 5, not an earlier or partial version. |

## Expected Final State

Project Settings' "Default Chat Configuration" list can be freely edited (add/remove, any mix of agents and pipelines), and the saved state is what new chats actually use.

## Pass/Fail Criteria

**Pass:**
- Steps 2–5 all persist correctly across reload
- Step 6 shows the exact edited set, not a stale one

**Fail:**
- Any add/edit is silently dropped or requires a specific type/count that isn't documented as a restriction
- New chat participants don't match what's currently saved in project settings
