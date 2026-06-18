---
id: ELITEA-0954
title: "Project Context Is Injected in Direct Chat Conversations"
priority: critical
type: functional
module: project-context
status: ready
execution_type: manual
tags: [project-context, private-project, feat:settings, team-project, story:3395, r-2.0.4, chat]
requirements: [EliteaAI/elitea_issues#3395]
---
# ELITEA-0954: Project Context Is Injected in Direct Chat Conversations

**Module:** Project Context · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that Project Context is injected into direct Chat conversations when the toggle is ON, for both Private and Team projects.

**Coverage:**
- Context injected in Private project Chat
- Context injected in Team project Chat
- Context NOT injected when toggle is OFF
- Context injected once per conversation, not duplicated per turn

## Preconditions

- Logged in to ELITEA (`{{base_url}}`)

## Test Data

- Project Context phrase: `QA-TEST-PHRASE: Silver wolf howls at dusk`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Set Project Context to 'QA-TEST-PHRASE: Silver wolf howls at dusk'. Toggle = ON. Save. | Content and toggle saved. |
| 2 | Open Chat in the Private project. Start a new conversation. Ask: 'What is the QA-TEST-PHRASE?' | Chat returns: 'Silver wolf howls at dusk'. |
| 3 | Repeat the same in a Team project. | Chat returns the phrase in the Team project as well. |
| 4 | Set toggle = OFF. Open a new chat conversation. Ask the same question. | Chat does NOT return the phrase. |
| 5 | Set toggle = ON. Send 5 messages in one conversation, then ask the phrase question again. | Phrase is returned correctly. Context is injected only once — not repeated/duplicated with each turn. |

## Expected Final State

Phrase is returned correctly. Context is injected only once — not repeated/duplicated with each turn.

## Pass/Fail Criteria

**Pass:**
- Chat returns phrase in both Private and Team projects with toggle ON
- Chat does not return phrase with toggle OFF
- Context appears once per conversation, not per message

**Fail:**
- Phrase not returned with toggle ON
- Phrase returned with toggle OFF
- Context duplicated per turn
