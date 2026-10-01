---
id: ELITEA-0395
title: "No @Mention Notification in Private Workspace — User Cannot Be Added to Chat"
priority: medium
type: functional
module: chat-interface
status: ready
execution_type: manual
tags: [feat:chat, r-2.0.7]
requirements: [EliteaAI/elitea_issues#4167, EliteaAI/elitea_issues#6368]
---
# ELITEA-0395: No @Mention Notification in Private Workspace — User Cannot Be Added to Chat

**Module:** Chat Interface · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that in a Private project, users cannot be added to a chat conversation and no other team members appear in the + suggestion dropdown, preventing any user mention notifications from being generated.

**Coverage:**
- "Add users" option is not available in Private project chat participants panel
- No team members appear in the + suggestion dropdown in Private project chat
- No erroneous user mention notification is received by any other user from a Private project chat

## Preconditions

- User A has access to their Private project
- User B exists in the system as a member of at least one shared Team Project

## Test Data

- User A: owner of a Private project
- User B: member of at least one shared Team Project with User A

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Log in as User A. Navigate to the Private project chat (not a Team Project). | Private project chat is open. |
| 2 | In the PARTICIPANTS panel, click the users icon to open the users dropdown. | Users dropdown opens. |
| 3 | Check whether the 'Add users' option is present in the dropdown. | 'Add users' option is NOT present — user collaboration is disabled in Private workspace. |
| 4 | In the chat input field, type @user_b_name (a known team member's username) and observe the input behavior. | No other team member can be referenced or tagged — the typed user mention is treated as plain text or goes unresolved. |
| 5 | Log out. Log in as User B. Navigate to the Notification tab. | User B's Notification tab is open. |
| 6 | Verify no user mention notification exists originating from User A's Private project. | Notification tab shows no notification from User A's Private project. |

## Expected Final State

Notification tab shows no notification from User A's Private project.

## Pass/Fail Criteria

**Pass:**
- "Add users" option is absent from the participants dropdown in Private project chat
- No other team member usernames appear in the + suggestion list in Private project chat
- User B receives no user mention notification from a Private project

**Fail:**
- "Add users" is available in Private project chat
- Other users appear in the + suggestion dropdown in a Private project chat
- User B receives a notification from a Private project user mention attempt
