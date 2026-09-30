---
id: ELITEA-3461
title: "Toggle Between Public and Restricted Multiple Times"
priority: critical
type: functional
module: conversations
status: ready
execution_type: manual
tags: [feat:chat, access-control, restrict-access, make-public, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6283]
---
# ELITEA-3461: Toggle Between Public and Restricted Multiple Times

**Module:** Conversations · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that a conversation can be toggled between public and restricted states multiple times without issues.

## Preconditions

- Logged in to {{base_url}} as conversation creator/author
- A PRIVATE conversation exists
- Multiple project members exist

## Test Data

| Field | Value |
|-------|-------|
| User Role | Conversation Author |
| Initial State | Private |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Make conversation public | Icon turns green, all members can access |
| 2 | Verify public state | "Restrict access" visible in menu |
| 3 | Restrict access (keep only author + 1 user) | Icon turns grey, limited access |
| 4 | Verify restricted state | "Make public" visible in menu |
| 5 | Make public again | Icon turns green |
| 6 | Verify all project members can access | Multiple users can open |
| 7 | Restrict again (different participants) | Access limited again |
| 8 | Verify correct access | Only selected have access |
| 9 | Make public third time | Works correctly |
| 10 | Restrict third time | Works correctly |
| 11 | Check message history | All messages intact through toggles |
| 12 | Check conversation functionality | Full functionality preserved |

## Expected Final State

- Multiple toggles work correctly
- No data corruption
- Access rules applied correctly each time

## Teardown

- None required
