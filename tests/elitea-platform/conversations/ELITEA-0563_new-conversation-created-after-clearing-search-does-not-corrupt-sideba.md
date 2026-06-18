---
id: ELITEA-0563
title: "New Conversation Created After Clearing Search Does Not Corrupt Sidebar List"
priority: high
type: functional
module: conversations
status: draft
execution_type: manual
tags: [eng:frontend, eng:backend, feat:chat, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4835]
---
# ELITEA-0563: New Conversation Created After Clearing Search Does Not Corrupt Sidebar List

**Module:** Conversations · **Priority:** High · **Type:** Functional

**Objective:** Verify that creating a new conversation immediately after using search and clearing it does not cause duplicate entries or missing conversations in the sidebar.

**Coverage:**
- New conversation appears exactly once in the Today date group after creation
- No existing conversations are missing from the list
- Sidebar list is not broken or blank after the create-after-search workflow

## Preconditions

- Logged in to {{base_url}} in the Private project

## Test Data

Search term: test | First message: Hello

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the Chat page, activate search, and type 'test' | Search results appear in the sidebar |
| 2 | Clear the search field completely | Normal conversation list is restored with date groups |
| 3 | Click the '+ Create' button in the sidebar | Chat input field is highlighted and focused |
| 4 | Type 'Hello' and press Enter to send the first message | New conversation is created and appears in the sidebar |
| 5 | Inspect the full sidebar conversation list | New conversation appears exactly once in the Today group; no duplicate entries exist; no other conversations are missing |

## Expected Final State

New conversation appears exactly once in the Today group; no duplicate entries exist; no other conversations are missing

## Pass/Fail Criteria

**Pass:**
- New conversation appears once in Today group
- No duplicates; no missing conversations
- Sidebar list is intact

**Fail:**
- New conversation appears twice (duplicate)
- Existing conversations disappear from the list
- Sidebar list is blank or broken
