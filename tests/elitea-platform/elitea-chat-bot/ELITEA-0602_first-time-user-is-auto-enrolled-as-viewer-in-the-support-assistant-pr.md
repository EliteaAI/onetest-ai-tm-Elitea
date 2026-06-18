---
id: ELITEA-0602
title: "First-time user is auto-enrolled as viewer in the Support Assistant project on first API call"
priority: high
type: functional
module: elitea-chat-bot
status: ready
execution_type: manual
tags: [auto-enrollment, hidden-project, viewer-role, story:4781, r-2.0.3]
requirements: [4781, 4773]
---
# ELITEA-0602: First-time user is auto-enrolled as viewer in the Support Assistant project on first API call

**Module:** Elitea Chat Bot · **Priority:** High · **Type:** Functional

**Objective:** Verify that a brand-new user who has never used the Support Assistant is automatically enrolled in the hidden Support Assistant project when they make their first API call to GET /v2/support_assistant/conversations. The call must succeed (not 403), the user must be assigned the viewer role, and the hidden project must not appear in their project list.

## Preconditions

A brand-new user account that has never previously used the Support Assistant.
Support Assistant is enabled.
Authenticated Bearer token for the new user.

## Test Data

New user Bearer token (account with no prior support history)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Send GET /v2/support_assistant/conversations with the new user's Bearer token | HTTP 200 response (not 403); empty array or no conversations (no error) |
| 2 | Verify the auto-enrollment happened: check via admin or project API if user is now enrolled in the Support Assistant project | User appears with viewer role in the Support Assistant project (admin verification) |
| 3 | Confirm the hidden project does NOT appear in the user's project list | GET /v2/elitea_core/projects or equivalent does NOT include the Support Assistant project for this user |
| 4 | Create a support conversation for this user and send a message | 201 and 200 responses; conversation and message created successfully |

## Expected Final State

201 and 200 responses; conversation and message created successfully

## Pass/Fail Criteria

PASS: First GET returns 200; user enrolled with viewer role; project not in user's list; conversation and messaging work.
FAIL: First GET returns 403; user must be manually enrolled; or hidden project appears in user's project list.
