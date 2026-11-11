---
id: ELITEA-4633
title: "ELITEA-4633: Run Skill from Catalog Skills Page and Verify Message Exchange"
priority: critical
type: regression
module: skills/catalog
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:skills, catalog, skill-run, chat]
requirements: [EliteaAI/elitea_issues#6922]
---
# ELITEA-4633: Run Skill from Catalog Skills Page and Verify Message Exchange

**Module:** Skills / Catalog · **Priority:** Critical · **Type:** Regression

**Objective:** Verify the complete flow of running a skill from Catalog → Skills page: clicking Run button creates a new chat with the skill as a participant, user can send a message, and skill responds successfully.

**Coverage:**
- Navigate to Catalog → Skills tab
- Skills display with Run button (play icon)
- Clicking Run creates new chat
- Skill added as participant with "Catalog" badge
- User can type and send message
- Skill executes and returns response
- Complete message exchange workflow

## Preconditions

- User is logged into {{base_url}}
- User has access to Catalog (Settings → Catalog menu visible)
- Catalog has at least one published skill available (e.g., "code-reviewer")

## Test Data

| Field | Value |
|-------|-------|
| Catalog skill | code-reviewer (or any published catalog skill) |
| Test message | "Review this code: function add(a, b) { return a + b; }" |
| Expected | Skill responds with code review feedback |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Catalog page (click "Catalog" in left sidebar) | Catalog page loads showing "Welcome to ELITEA Catalog!" |
| 2 | Click on "Skills" tab in the Catalog page | Skills tab becomes active, displaying list of published catalog skills |
| 3 | Locate a catalog skill card (e.g., "code-reviewer") | Skill card displays with skill name, icon, and Run button (play icon ▶) |
| 4 | Hover over the Run button on the skill card | Run button highlights (if applicable) |
| 5 | Click the Run button (play icon ▶) on the skill card | Action triggers and page navigates to chat interface |
| 6 | Observe the chat interface loads | New chat opens with greeting message (e.g., "Hello, Mariam! What can I do for you today?") |
| 7 | Check right panel PARTICIPANTS section | In PARTICIPANTS → SKILLS section, catalog skill appears as participant with "Catalog" badge (e.g., "code-r... Catalog v1.0") |
| 8 | Verify chat input field is ready | Chat input field is active and displays placeholder "Type your message..." |
| 9 | Type a message in the input field: "Review this code: function add(a, b) { return a + b; }" | Message appears in input field |
| 10 | Click the send button (arrow icon →) or press Enter | Message sends successfully and appears in chat thread |
| 11 | Wait for skill response | Skill processes the message |
| 12 | Observe skill response appears in chat | Skill returns response (e.g., code review feedback) in chat thread |
| 13 | Verify response is relevant to the sent message | Response content is appropriate for the skill's purpose (code review feedback for code-reviewer skill) |
| 14 | Check left sidebar Chats list | New chat appears in Chats list |

## Expected Final State

- New chat created from Catalog → Skills → Run button
- Catalog skill added as participant in PARTICIPANTS → SKILLS section with "Catalog" badge
- User successfully sent message to skill
- Skill executed and returned relevant response
- Chat appears in Chats list
- Complete bidirectional communication established

## Pass/Fail Criteria

**Pass:**
- Run button on Catalog skill card creates new chat
- Skill appears as participant with "Catalog" badge and version
- User can send message to skill
- Skill responds with relevant output
- Chat saved in Chats list

**Fail:**
- Run button doesn't create new chat
- Skill not added as participant
- Cannot send message to skill
- Skill doesn't respond or response is error
- Chat not saved in Chats list

## Notes

**Source functional tests:** ELITEA-4240, ELITEA-4242
**Regression rationale:** Complete end-to-end workflow for running catalog skills; validates Run button functionality, chat creation, participant setup, and bidirectional message exchange.
**Selected checkpoints:** Catalog navigation, Run button click, chat creation, participant display, message send, skill response.
**Extends:** This test extends ELITEA-4253 by adding the message exchange verification after chat creation.
