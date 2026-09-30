---
id: ELITEA-3445
title: "Successfully Make Conversation Public"
priority: critical
type: functional
module: conversations
status: ready
execution_type: manual
tags: [feat:chat, access-control, make-public, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6283]
---
# ELITEA-3445: Successfully Make Conversation Public

**Module:** Conversations · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that a private conversation can be successfully made public and all project members gain access.

## Preconditions

- Logged in to {{base_url}} as conversation creator/author
- A private conversation exists in a team project
- At least one other project member exists who currently cannot access the conversation

## Test Data

| Field | Value |
|-------|-------|
| User Role | Conversation Author |
| Initial State | Private conversation |
| Other Users | At least 1 project member |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Note the conversation's sharing icon color | Icon is grey (private) |
| 2 | Right-click on the private conversation | Action dropdown menu opens |
| 3 | Click "Make public" option | Confirmation dialog appears |
| 4 | Verify dialog content | Title: "Public conversation?", Message: "Are you sure to make your conversation public?" |
| 5 | Click "Make public" button | Dialog closes |
| 6 | Observe sharing icon immediately | Icon turns GREEN immediately (no refresh needed) |
| 7 | Right-click conversation again | "Make public" option is NO LONGER visible |
| 8 | Verify "Restrict access" is visible | "Restrict access" option appears in dropdown |
| 9 | Login as another project member | Member CAN now access and open the conversation |
| 10 | Verify conversation content accessible | All messages visible to the new member |

## Expected Final State

- Conversation is public
- Sharing icon displays green
- All project members have access
- "Make public" hidden, "Restrict access" visible in dropdown

## Teardown

- Optionally restrict access back to restore original state
