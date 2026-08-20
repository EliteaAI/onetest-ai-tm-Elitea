---
id: ELITEA-2670
title: "Verify behavior when toggle disabled mid-conversation with existing mid-turn history"
priority: medium
type: functional
module: default-modules
status: ready
execution_type: manual
tags: [feat:chat, eng:backend, eng:frontend, eng:sdk, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6115]
---

## Preconditions

- User is logged in to `{{base_url}}`
- Mid-turn Input (Beta) toggle is enabled
- Conversation has existing mid-turn interaction history

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/chat` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Verify conversation has mid-turn messages in history | "Sent while running" labels visible |
| 2 | Navigate to Settings and disable Mid-turn Input toggle | Toggle switched to OFF |
| 3 | Return to the conversation | Conversation loads |
| 4 | Verify existing mid-turn history preserved | Old "sent while running" labels still visible |
| 5 | Start a new agent turn | Agent starts |
| 6 | Verify input field is now disabled during turn | Cannot send mid-turn messages |

## Expected Final State

Existing mid-turn history is preserved when toggle is disabled, but new interactions follow the disabled state.

## Pass/Fail Criteria

**Pass:**
- Existing history preserved with labels
- New interactions respect toggle OFF state

**Fail:**
- History labels disappear
- Toggle change corrupts conversation
