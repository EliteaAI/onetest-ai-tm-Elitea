---
id: ELITEA-0175
title: "Agent Author Receives Notification With Reason When Platform Admin Unpublishes Their Agent"
priority: medium
type: functional
module: agents-publishing
status: draft
execution_type: manual
tags: [feat:agents, story:3773, r-2.0.2]
requirements: [ProjectAlita/projectalita.github.io#3773]
---
# ELITEA-0175: Agent Author Receives Notification With Reason When Platform Admin Unpublishes Their Agent

**Module:** Agents Publishing · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that the original author of an agent receives a notification in their Notification Center when a platform admin unpublishes their agent — and that the notification includes the agent name and the admin-provided reason.

**Coverage:**
- Notification delivered to originating author after admin unpublish
- Notification contains agent name
- Notification contains the specific reason provided by admin
- Notification is NOT shown to other non-author users in the same project

## Preconditions

- User A is the author of Agent P on {{base_url}}
- Platform Admin has access to unpublish Agent P
- User C is another project member who is not the author of Agent P

## Test Data

- Unpublish reason: "Violates platform content rules"
- Agent name: Agent P's exact name (note from environment)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Platform Admin unpublishes Agent P using reason "Violates platform content rules" | Unpublish completes successfully |
| 2 | Log in as User A (the agent author) | User A's session is active |
| 3 | Click the Notifications bell icon in the sidebar | Notifications panel opens |
| 4 | Look for a notification related to Agent P's unpublish event | A notification entry is visible for the unpublish event |
| 5 | Read the notification content | Notification contains: Agent P's name AND the reason "Violates platform content rules" |
| 6 | Log in as User C (another project member, not the author) | User C's session active |
| 7 | Open User C's Notifications panel | Notifications panel opens |
| 8 | Search for any notification about Agent P's unpublish | No such notification is visible to User C |

## Expected Final State

No such notification is visible to User C

## Pass/Fail Criteria

**Pass:**
- User A receives a notification about their agent being unpublished
- Notification contains both the agent name and the admin-provided reason
- Non-author User C does not receive the notification

**Fail:**
- User A receives no notification after admin unpublish
- Notification is missing the agent name or the unpublish reason
- Non-author User C also receives the notification (notification leaked to wrong user)
- Notification arrives but shows incorrect agent or reason
