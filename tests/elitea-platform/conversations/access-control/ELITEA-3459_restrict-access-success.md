---
id: ELITEA-3459
title: "Successfully Restrict Access via Wizard"
priority: critical
type: functional
module: conversations
status: ready
execution_type: manual
tags: [feat:chat, access-control, restrict-access, wizard, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6283]
---
# ELITEA-3459: Successfully Restrict Access via Wizard

**Module:** Conversations · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that clicking the "Restrict access" button successfully restricts the conversation to selected participants only.

## Preconditions

- Logged in to {{base_url}} as conversation creator/author
- A PUBLIC conversation exists with User A (author), B, C, D, E

## Test Data

| Field | Value |
|-------|-------|
| User A | Conversation Author |
| Users B, C | To retain access |
| Users D, E | To remove access |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open Restrict Access wizard | All 5 participants displayed |
| 2 | Remove User D and User E | D and E chips removed |
| 3 | Verify remaining: A (author), B, C | 3 users remain selected |
| 4 | Click "Restrict access" button | Processing may show briefly |
| 5 | Wizard closes | Modal dismissed |
| 6 | Verify success indication | Toast/notification or visual confirmation |
| 7 | Check sharing icon | Icon should turn GREY (restricted) |
| 8 | Open dropdown menu | "Make public" option now visible |
| 9 | Login as User D | Login successful |
| 10 | Try to access conversation | Access DENIED |
| 11 | Login as User B | Login successful |
| 12 | Access conversation | Access GRANTED, full functionality |

## Expected Final State

- Conversation restricted to A, B, C only
- D and E lost access immediately
- UI reflects new restricted state

## Teardown

- None required
