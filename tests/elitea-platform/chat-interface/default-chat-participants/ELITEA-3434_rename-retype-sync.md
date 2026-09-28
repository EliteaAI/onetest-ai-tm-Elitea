---
id: ELITEA-3434
title: "Renaming or Retyping a Preconfigured Agent/Pipeline Syncs Into Default Chat Configuration"
priority: low
type: functional
module: chat
status: draft
execution_type: manual
tags: [feat:chat, story:6358, default-chat-config, regression]
requirements: [EliteaAI/elitea_issues#6358]
---
# ELITEA-3434: Renaming or Retyping a Preconfigured Agent/Pipeline Syncs Into Default Chat Configuration

**Module:** Chat · **Priority:** Low · **Type:** Functional

**Objective:** Confirm renaming or retyping an agent/pipeline that is a preconfigured participant correctly syncs its stored name/type in `chat_config.participants`, and that a user without configuration-edit permission triggers no error on save.

**Coverage:** Regression — `EliteaUI#1084`.

## Preconditions

- A project with an agent configured as a preconfigured participant
- A second user account without permission to edit project configuration (e.g. Editor)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | As an admin/user with configuration-edit permission, rename the preconfigured agent and Save. | Save succeeds. |
| 2 | Open a new chat. | The preconfigured participant shows the **updated name**, not the old one. |
| 3 | Where applicable, change the agent's type and Save. | Save succeeds; a subsequent new chat reflects the updated type. |
| 4 | As the Editor-role user (no configuration-edit permission), make an unrelated valid change to the same agent (e.g. edit its description) and Save. | Save succeeds normally with no error — the participant-list sync silently no-ops rather than blocking the save. |

## Expected Final State

Renaming/retyping a preconfigured agent or pipeline is correctly reflected in subsequent new chats; users without configuration-edit permission can still save their own changes without being blocked by the sync logic.

## Pass/Fail Criteria

**Pass:**
- Steps 2 and 3 show updated name/type
- Step 4 succeeds with no error shown to the Editor-role user

**Fail:**
- New chats still show the old name/type after a rename
- Step 4 fails or errors for the Editor-role user
