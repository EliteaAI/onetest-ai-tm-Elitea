---
id: ELITEA-0948
title: "Project Context Is Injected for Agent Added as Chat Participant"
priority: critical
type: functional
module: project-context
status: ready
execution_type: manual
tags: [project-context, private-project, feat:settings, team-project, story:3395, r-2.0.4, agents, chat]
requirements: [EliteaAI/elitea_issues#3395]
---
# ELITEA-0948: Project Context Is Injected for Agent Added as Chat Participant

**Module:** Project Context · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that Project Context is injected for an agent when it is added as a participant to a Chat page conversation.

**Coverage:**
- Newly created agent receives context via Chat page
- Existing agent receives context via Chat page
- Works in both Private and Team projects
- Context not injected when toggle is OFF

## Preconditions

- Logged in to ELITEA (`{{base_url}}`)

## Test Data

- Project Context phrase: `QA-TEST-PHRASE: Red kite soars at midday`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Set Project Context to 'QA-TEST-PHRASE: Red kite soars at midday'. Toggle = ON. Save. | Content and toggle saved. |
| 2 | Open the Chat page. Start a new conversation. Add a newly created agent as a participant to the conversation. | Agent is added as a participant. |
| 3 | Ask: 'What is the QA-TEST-PHRASE?' | Agent returns: 'Red kite soars at midday'. |
| 4 | Start a new conversation. Add an existing other (previously created) agent as a participant (very old one). Ask the same question. | Existing agent also returns the phrase. |
| 5 | Test in both Private and Team projects. | Context injection works in both project types. |
| 6 | Set toggle = OFF. Add agent to a new chat. Ask the same question. | Agent does NOT return the phrase. |

## Expected Final State

Agent does NOT return the phrase.

## Pass/Fail Criteria

**Pass:**
- Agent added as Chat participant returns the phrase with toggle ON
- Both new and existing agents receive context
- Works in Private and Team projects
- No injection when toggle is OFF

**Fail:**
- Agent in chat does not return the phrase with toggle ON
- Context injected when toggle is OFF
