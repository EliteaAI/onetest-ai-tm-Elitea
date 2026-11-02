---
id: ELITEA-4271
title: "Tilde Mention Skill in Chat Without Agent"
priority: critical
type: functional
module: chat/skills
status: ready
execution_type: manual
tags: [user_story:6924, feat:skills, feat:chat-participants, skills-as-participants, mentions]
requirements: [EliteaAI/elitea_issues#6924]
---
# ELITEA-4271: Tilde Mention Skill in Chat Without Agent

**Module:** Chat / Skills · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that typing `~` (tilde) in a chat without an agent displays a mention dropdown listing skill participants, and selecting a skill inserts the mention into the message.

## Preconditions

- User is logged into https://next.elitea.ai/app/
- A chat session is open WITHOUT an agent participant
- At least one skill participant is added to the chat (e.g., "jira-skill")
- Skill participant is visible in PARTICIPANTS panel

## Test Data

| Chat Type | Skill Participant | Mention Trigger | Expected Dropdown Section |
|-----------|-------------------|-----------------|---------------------------|
| Chat without agent | jira-skill | `~` | MENTION SKILL section with "jira-skill" |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Verify the chat session has NO agent participant (PARTICIPANTS panel shows only skills) | No agent is present, only skill participants visible |
| 2 | Verify at least one skill participant (e.g., "jira-skill") is in the PARTICIPANTS panel | Skill participant "jira-skill" is visible |
| 3 | Click in the chat input field to focus it | Input field is focused and ready for typing |
| 4 | Type `~` (tilde character) in the input field | Mention dropdown appears immediately below the cursor |
| 5 | Verify the dropdown displays "MENTION SKILL" section header | "MENTION SKILL" section is visible in the dropdown |
| 6 | Verify the skill participant(s) are listed in the dropdown (e.g., "jira-skill") | Skill participant "jira-skill" appears in the list |
| 7 | Click on the skill participant in the dropdown (e.g., "jira-skill") | Mention is inserted into the input field as `~jira-skill` (or formatted mention) |
| 8 | Verify the dropdown closes after selection | Dropdown is dismissed |
| 9 | Type additional text after the mention (e.g., `~jira-skill please list projects`) | Text is added after the mention, input field contains full message |
| 10 | Send the message and verify it is posted with the mention intact | Message is sent with the skill mention visible |

## Expected Final State

- Tilde `~` triggers mention dropdown in chats without agents
- Dropdown displays "MENTION SKILL" section with skill participants
- Selecting a skill inserts the mention into the input field
- Message can be sent with the skill mention

## Pass/Fail Criteria

**Pass:**
- Typing `~` in chat without agent triggers mention dropdown
- "MENTION SKILL" section header is displayed
- Skill participants are listed in the dropdown
- Clicking a skill inserts the mention into the input field
- Dropdown closes after selection
- Message with mention can be sent successfully

**Fail:**
- Tilde `~` does not trigger mention dropdown
- "MENTION SKILL" section is missing or incorrect
- Skill participants are not listed in dropdown
- Clicking a skill does not insert mention or inserts incorrectly
- Dropdown remains open after selection
- Message with mention cannot be sent
