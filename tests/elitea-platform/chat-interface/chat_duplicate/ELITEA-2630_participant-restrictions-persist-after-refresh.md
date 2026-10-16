---
id: ELITEA-2630
title: "Participant Restrictions Enforced After Refresh and API Access"
priority: medium
type: functional
module: chat-interface
status: ready
execution_type: manual
tags: [chat, duplicate, participants, persistence, P1]
requirements: [3837]
---
# ELITEA-2630: Participant Restrictions Enforced After Refresh and API Access

**Module:** Chat Interface · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that participant restrictions in a duplicated chat remain enforced after page refresh and through any available API or alternate entry point.

## Preconditions

- User is logged in to {{base_url}}
- Duplicated chat exists with specific participants
- Original participant list documented

## Test Data

- URL: {{base_url}}
- Duplicated chat with: User A, User B, Agent X
- NOT including: User C (team member)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open duplicated chat and document participants | User A, User B, Agent X present |
| 2 | Refresh the browser page (F5) | Page reloads |
| 3 | Re-open the duplicated chat | Chat opens successfully |
| 4 | Verify participants remain unchanged | Same participants: User A, User B, Agent X |
| 5 | Verify User C still not present | User C not added after refresh |
| 6 | Log out and log back in | Session refreshed |
| 7 | Open duplicated chat again | Chat accessible |
| 8 | Verify participant list unchanged | Participants still restricted to original set |
| 9 | User C: Attempt to access the non-public chat (if applicable) | Access denied or chat not visible |
| 10 | Verify participant restrictions persist across sessions | Restrictions maintained |

## Expected Final State

- Participant list unchanged after refresh
- Restrictions enforced across sessions
- Unauthorized users cannot access chat
- Participant integrity maintained

## Pass/Fail Criteria

**Pass:**
- Participants unchanged after refresh
- Restrictions persist across logout/login
- User C cannot access non-public chat
- Participant list stable and enforced
- No degradation of access control

**Fail:**
- Participants change after refresh
- Restrictions not enforced after login
- User C gains access unexpectedly
- Participant list contaminated
- Access control fails
