---
id: ELITEA-4634
title: "ELITEA-4634: Run Own Skill from Skills Page and Verify Message Exchange"
priority: critical
type: regression
module: skills
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:skills, skill-run, chat, my-skills]
requirements: [EliteaAI/elitea_issues#6922]
---
# ELITEA-4634: Run Own Skill from Skills Page and Verify Message Exchange

**Module:** Skills · **Priority:** Critical · **Type:** Regression

**Objective:** Verify the complete flow of running a user's own skill from the Skills page: clicking Run button creates a new chat with the skill as a participant, user can send a message, and skill responds successfully.

**Coverage:**
- Navigate to Skills page (user's own skills)
- Skills display with Run button
- Clicking Run creates new chat
- Skill added as participant (without "Catalog" badge)
- User can type and send message
- Skill executes and returns response
- Complete message exchange workflow for own skills

## Preconditions

- User is logged into {{base_url}}
- User has created at least one skill (e.g., "jira-skill", "uppercase-text-converter")
- Skill has valid instructions and is in ready state

## Test Data

| Field | Value |
|-------|-------|
| Own skill | uppercase-text-converter (or any user's own skill) |
| Test message | "Convert this to uppercase: hello world" |
| Expected | Skill responds with "HELLO WORLD" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Skills page (click "Skills" in left sidebar) | Skills page loads showing user's own skills list |
| 2 | Locate one of user's own skills (e.g., "uppercase-text-converter") | Skill card or row displays with skill name and Run button (play icon ▶) |
| 3 | Identify that the skill is user's own skill (no "Catalog" badge) | Skill card shows user's skill without "Catalog" badge |
| 4 | Click the Run button (play icon ▶) on the skill | Action triggers and page navigates to chat interface |
| 5 | Observe the chat interface loads | New chat opens with greeting or empty chat ready for input |
| 6 | Check right panel PARTICIPANTS section | In PARTICIPANTS → SKILLS section, skill appears as participant with version badge (e.g., "uppercase... v1" or "base") |
| 7 | Verify NO "Catalog" badge is displayed for own skill | Skill participant shows version badge but NOT "Catalog" badge (distinguishes from catalog skills) |
| 8 | Verify chat input field is ready | Chat input field is active and displays placeholder "Type your message..." |
| 9 | Type a message in the input field: "Convert this to uppercase: hello world" | Message appears in input field |
| 10 | Click the send button (arrow icon →) or press Enter | Message sends successfully and appears in chat thread |
| 11 | Wait for skill response | Skill processes the message |
| 12 | Observe skill response appears in chat | Skill returns response (e.g., "HELLO WORLD") in chat thread |
| 13 | Verify response is relevant and correct | Response content matches skill's purpose (uppercase conversion) |
| 14 | Check left sidebar Chats list | New chat appears in Chats list |

## Expected Final State

- New chat created from Skills page → Run button
- Own skill added as participant in PARTICIPANTS → SKILLS section WITHOUT "Catalog" badge
- User successfully sent message to skill
- Skill executed and returned correct response
- Chat appears in Chats list
- Complete bidirectional communication established

## Pass/Fail Criteria

**Pass:**
- Run button on own skill creates new chat
- Skill appears as participant with version badge but WITHOUT "Catalog" badge
- User can send message to skill
- Skill responds with relevant and correct output
- Chat saved in Chats list

**Fail:**
- Run button doesn't create new chat
- Skill not added as participant
- Own skill incorrectly shows "Catalog" badge
- Cannot send message to skill
- Skill doesn't respond or response is error
- Chat not saved in Chats list

## Notes

**Source functional tests:** ELITEA-4240, ELITEA-4242
**Regression rationale:** Complete end-to-end workflow for running user's own skills; validates Run button functionality for non-catalog skills, chat creation, and distinguishes own skills from catalog skills by badge absence.
**Selected checkpoints:** Skills page navigation, Run button click, chat creation, participant display (no "Catalog" badge), message send, skill response.
**Distinguishes from:** ELITEA-4633 tests catalog skills (with "Catalog" badge); this tests own skills (without "Catalog" badge).
