---
id: ELITEA-0610
title: "Support Assistant opened from sidebar and from floating launcher share the same session"
priority: high
type: functional
module: elitea-chat-bot
status: ready
execution_type: manual
tags: [entry-point-parity, session-sharing, story:4780, launcher, r-2.0.3, sidebar]
requirements: [4780, 4774]
---
# ELITEA-0610: Support Assistant opened from sidebar and from floating launcher share the same session

**Module:** Elitea Chat Bot · **Priority:** High · **Type:** Functional

**Objective:** Verify that the sidebar entry point and the floating launcher entry point both open the same Support Assistant session. If a user sends a message from one entry point and then opens the assistant from the other entry point, they must see the same conversation — not two separate instances.

## Preconditions

Support Assistant is enabled and appears in both the sidebar and as a floating launcher.
Tester is logged in as a regular user.

## Test Data

Message sent via floating launcher: "Launched from floating icon"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Click the floating launcher to open the Support Assistant | Panel opens |
| 2 | Send message: "Launched from floating icon" | Message sent; response received |
| 3 | Close the panel by clicking X | Panel closes |
| 4 | Click the sidebar Support Assistant entry | The Support Assistant panel opens |
| 5 | Verify the conversation area | "Launched from floating icon" and its response are visible — same session as opened from the launcher |

## Expected Final State

"Launched from floating icon" and its response are visible — same session as opened from the launcher

## Pass/Fail Criteria

PASS: Same messages visible regardless of which entry point is used to open the panel.
FAIL: Sidebar opens a fresh/empty session; floating launcher and sidebar show different conversations.
