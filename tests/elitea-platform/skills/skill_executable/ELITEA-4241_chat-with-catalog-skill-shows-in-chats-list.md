---
id: ELITEA-4241
title: Chat with Catalog skill participant appears in Chats list
priority: critical
type: functional
module: elitea-platform
status: ready
execution_type: manual
tags: [feat:skills, skill-run, catalog, chat, persistence, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6922]
---
# ELITEA-4241: Chat with Catalog skill participant appears in Chats list

**Module:** Elitea Platform · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that after running a Catalog skill, the created chat appears in the Chats list and can be reopened.

**Coverage:**
- Chat appears in Chats list
- Chat has proper name/title
- Chat can be clicked to reopen
- Skill participant remains attached

## Preconditions

- User is logged in to {{base_url}}
- User has clicked Run on a Catalog skill
- New chat with skill participant was created

## Test Data

- Previously created chat with Catalog skill participant
- Expected: Chat visible in Chats list, clickable

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | After running Catalog skill and chat is created, look at left sidebar | Left sidebar shows "Chats" section |
| 2 | Check the Chats list for the newly created chat | New chat appears in the Chats list |
| 3 | Observe the chat name/title | Chat has a generated name (e.g., skill name "animal-joke" or first message content) |
| 4 | Check the chat position in the list | Chat appears at the top (most recent chats first) |
| 5 | Click on the chat item in the Chats list | Chat opens in main chat interface |
| 6 | Verify skill participant is still attached | Right panel shows skill in SKILLS participant section |
| 7 | Navigate away to another page, then return to Chats | Chat still appears in Chats list |

## Expected Final State

Chat with Catalog skill participant is visible in Chats list, has proper name, and can be reopened by clicking.

## Pass/Fail Criteria

**Pass:** Chat appears in Chats list with proper name, clicking reopens it with skill participant intact.

**Fail:** Chat missing from list, incorrect name, or clicking doesn't reopen properly.
