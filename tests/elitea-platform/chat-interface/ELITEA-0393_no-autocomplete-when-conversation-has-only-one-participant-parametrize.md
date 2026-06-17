---
id: ELITEA-0393
title: "No autocomplete when conversation has only one participant [Parametrized: personal project / team project solo chat]"
priority: high
type: functional
module: chat-interface
status: ready
execution_type: manual
tags: [feat:chat, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4896]
---
# ELITEA-0393: No autocomplete when conversation has only one participant [Parametrized: personal project / team project solo chat]

**Module:** Chat Interface · **Priority:** High · **Type:** Functional

**Objective:** Verify that typing `@` in a chat where you are the only participant does not trigger an autocomplete dropdown, and that the application handles this gracefully without errors.

**Coverage:**
- No dropdown appears in a personal project chat with a single participant (yourself)
- No dropdown appears in a team project chat where only you have participated in this specific conversation
- `@` is accepted as plain text without triggering any UI element
- Normal message sending is unaffected

## Preconditions

- Logged into ELITEA at {{base_url}}

**Scenario 1:** A personal/private project chat where only you are the participant
**Scenario 2:** A team project chat where only you have participated in this specific conversation (no other member has been added or written in it)

## Test Data

| # | Scenario | Project type | Participants in this chat |
|---|---|---|---|
| 1 | Personal project | Personal / private | 1 (only you) |
| 2 | Team project, solo chat | Team project | 1 (only you — no other members added or wrote in this specific chat) |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the chat for Scenario 1 (personal project chat) | Chat view loads; participants panel shows only you |
| 2 | Click the message input field and type `@` | No autocomplete dropdown appears; `@` is shown as plain text in the input |
| 3 | Continue typing `test` (input is now `@test`) | Still no dropdown; `@test` is in the field as plain text |
| 4 | Clear the input; send a regular message without `@` | Message is sent successfully; normal chat functionality is unaffected |
| 5 | Repeat steps 1–4 for Scenario 2 (team project solo chat) | Identical results: no dropdown, `@` treated as plain text, messaging works normally |

## Expected Final State

Identical results: no dropdown, `@` treated as plain text, messaging works normally

## Pass/Fail Criteria

**Pass:**
- No dropdown appears in either scenario when there are no other participants
- `@` is treated as plain text without triggering any UI
- Standard messaging continues to work normally

**Fail:**
- An empty or broken dropdown appears when there are no other participants to suggest
- Application throws an error or crashes when `@` is typed with no participants
- Regular messaging stops working after typing `@`
