---
id: ELITEA-4253
title: Clicking Run on Catalog skill creates chat with skill as participant
priority: critical
type: regression
module: elitea-platform
status: draft
execution_type: manual
tags: [feat:skills, skill-run, catalog, chat, participant, regression, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6922]
---
# ELITEA-4253: Clicking Run on Catalog skill creates chat with skill as participant (Regression)

**Module:** Elitea Platform · **Priority:** Critical · **Type:** Regression

**Objective:** Verify that clicking Run button on a Catalog skill creates a new chat conversation with the skill added as a participant.

**Coverage:**
- Run button creates new chat
- Skill added as participant
- Chat appears in Chats list
- User can interact with skill in chat

## Preconditions

- User is logged in to {{base_url}}
- Catalog has at least one published skill (e.g., "animal-joke")
- User has permission to create chats

## Test Data

- Catalog skill: "animal-joke" with version "v8" (or any published skill)
- Expected: New chat created with skill as participant

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Catalog → Skills tab | Catalog Skills view displays published skills |
| 2 | Locate published skill "animal-joke" (or similar) | Skill card displays with Run button (play icon) |
| 3 | Click the Run button (play icon) on the skill card | Action triggers and navigates to new view |
| 4 | Observe what happens after clicking Run | A NEW chat conversation is created and opens |
| 5 | Check the chat interface for skill participant | Chat opens in main chat interface |
| 6 | Look at right panel "PARTICIPANTS" section under "SKILLS" | Catalog skill appears as participant with label "animal-j... Catalog v8" (or similar) |
| 7 | Check left sidebar Chats list | New chat appears in Chats list |
| 8 | Verify chat input is ready for messages | Chat input field is active and ready to accept messages |

## Expected Final State

New chat created with Catalog skill added as participant; chat appears in Chats list; user can send messages.

## Pass/Fail Criteria

**Pass:** Clicking Run creates new chat, skill added as participant in right panel SKILLS section, chat appears in Chats list.

**Fail:** Chat not created, skill not added as participant, or chat doesn't appear in list.
