---
id: ELITEA-3435
title: "Per-Chat Participant Edits Are Independent of Project Defaults and Persist on Duplicate"
priority: medium
type: functional
module: chat
status: draft
execution_type: manual
tags: [feat:chat, story:6358, default-chat-config, chat_duplicate]
requirements: [EliteaAI/elitea_issues#6358]
---
# ELITEA-3435: Per-Chat Participant Edits Are Independent of Project Defaults and Persist on Duplicate

**Module:** Chat · **Priority:** Medium · **Type:** Functional

**Objective:** Confirm a chat's participant list can be edited after creation without affecting the project-level "Default Chat Configuration", and that duplicating a chat carries over what was actually in that chat — not a fresh re-application of the project's defaults.

**Coverage:** AC — per-chat flexibility explicitly required alongside the auto-population behavior.

## Preconditions

- A project with 1+ preconfigured participants configured
- Access to the chat duplicate action

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open a new chat; confirm preconfigured participant(s) are pre-populated. | Participant panel matches project defaults. |
| 2 | In this specific chat, remove the default participant(s) and add a different agent/pipeline instead. Send a message. | The chat now uses the newly-selected participant, not the project default. |
| 3 | Open Project Settings → "Default Chat Configuration". | The project-level list is **unchanged** — the per-chat edit in step 2 did not modify project settings. |
| 4 | Duplicate the chat from step 2. | The duplicate opens with the **edited participant set from step 2** — not reset to the project's default participants. |
| 5 | Open a separate, brand-new chat (not a duplicate). | This new chat correctly pre-populates from the **project defaults** again, confirming step 2's edit was scoped only to that one chat. |

## Expected Final State

Per-chat participant edits are fully independent of the project-level default configuration; duplicating a chat preserves its actual (possibly edited) participant set rather than re-applying project defaults.

## Pass/Fail Criteria

**Pass:**
- Step 3 shows no change to project settings
- Step 4's duplicate matches step 2's edited set
- Step 5's fresh new chat matches the unmodified project defaults

**Fail:**
- Step 4's duplicate reverts to or re-adds the project's default participants instead of preserving the source chat's actual set
- Step 2's per-chat edit leaks into project settings
