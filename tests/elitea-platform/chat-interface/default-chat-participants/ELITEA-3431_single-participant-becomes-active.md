---
id: ELITEA-3431
title: "Exactly One Preconfigured Participant Becomes the Active Participant on a New Chat"
priority: medium
type: functional
module: chat
status: draft
execution_type: manual
tags: [feat:chat, story:6358, default-chat-config, new-chat]
requirements: [EliteaAI/elitea_issues#6358]
---
# ELITEA-3431: Exactly One Preconfigured Participant Becomes the Active Participant on a New Chat

**Module:** Chat · **Priority:** Medium · **Type:** Functional

**Objective:** Confirm the documented UI behavior — *"If exactly one is configured, it becomes the active participant"* — actually holds, and confirm the behavior when more than one is configured.

**Coverage:** AC — this exact rule is stated in the Settings UI's own helper text and needs direct verification rather than being taken on faith.

## Preconditions

- Admin access to Project Settings → "Default Chat Configuration"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure **exactly one** preconfigured participant (a single agent) and Save. | Save succeeds. |
| 2 | Open a new chat. | The one preconfigured agent is not just listed but becomes the **active participant** immediately — ready to receive the first message without further selection. |
| 3 | Send a message without changing anything. | Message is sent to that agent. |
| 4 | Go back to settings, add a **second** preconfigured participant (now two total), and Save. | Save succeeds. |
| 5 | Open another new chat. | Record actual behavior: is any one of the two auto-activated, or does the user need to pick which one is active? Document the observed behavior since it isn't specified beyond the single-participant case. |

## Expected Final State

With exactly one preconfigured participant, it is immediately active with no extra step. Behavior with 2+ is documented as observed, since the UI text only makes an explicit claim about the single-participant case.

## Pass/Fail Criteria

**Pass:**
- Step 2 shows the single participant already active, and step 3's message reaches it without an extra selection step

**Fail:**
- With exactly one participant configured, the new chat still requires the user to manually activate/select it despite the UI's own claim
