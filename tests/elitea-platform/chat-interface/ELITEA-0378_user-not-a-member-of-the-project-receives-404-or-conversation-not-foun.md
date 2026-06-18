---
id: ELITEA-0378
title: "User not a member of the project receives 404 or \"Conversation not found\" when accessing a chat URL belonging to that project"
priority: medium
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [nfr:usability, eng:frontend, feat:chat, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4374]
---
# ELITEA-0378: User not a member of the project receives 404 or "Conversation not found" when accessing a chat URL belonging to that project

**Module:** Chat Interface · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that a user who has no project membership for the target project sees a 404 error or the "Conversation not found" dialog when accessing a conversation URL from that project — and cannot view any conversation content.

**Coverage:**
- User with no project membership gets an error state (404 page or "Conversation not found" dialog), not a working conversation view
- No conversation messages, participant names, or project content from the target project are exposed
- User can still navigate back to their own projects and conversations after dismissing the error

## Preconditions

- Logged in as User C (an ELITEA user who is NOT a member of the project owning the conversation)
- User A has a conversation in their team project; the conversation URL is known
- User C has their own Private project with at least one conversation
- Environment: {{base_url}}

## Test Data

- Target conversation URL from a project User C is not a member of: e.g. {{base_url}}

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Log in as User C (non-member of User A's project) | User C is on the Chat page in their own Private project |
| 2 | Paste the conversation URL from User A's team project into the browser address bar and navigate to it | Page begins loading |
| 3 | Wait 2–3 seconds | A 404 error page is displayed |
| 4 | Inspect the error state content | No conversation messages, participant names, or project metadata from User A's project are visible |
| 5 | Open one of User C's own conversations from the sidebar | User C can open their own conversations and chat normally — no residual error state |

## Expected Final State

User C can open their own conversations and chat normally — no residual error state

## Pass/Fail Criteria

**Pass:**
- User C sees a 404 error page OR the "Conversation not found" dialog
- Zero data from the inaccessible project/conversation is visible at any point
- User C can return to their own project and continue working normally

**Fail:**
- User C can view the conversation content of a project they don't belong to
- No error state is shown (silent redirect or blank screen)
- Any project data from the inaccessible project leaks through to User C
