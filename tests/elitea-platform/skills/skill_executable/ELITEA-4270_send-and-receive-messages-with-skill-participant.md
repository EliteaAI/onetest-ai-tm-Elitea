---
id: ELITEA-4270
title: "Send and Receive Messages with Skill Participant"
priority: critical
type: functional
module: chat/skills
status: ready
execution_type: manual
tags: [user_story:6924, feat:skills, feat:chat-participants, skills-as-participants, streaming]
requirements: [EliteaAI/elitea_issues#6924]
---
# ELITEA-4270: Send and Receive Messages with Skill Participant

**Module:** Chat / Skills · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that messages can be sent to skill participants and responses are received with streaming, displaying "Thought for X secs", skill badge, and model badge.

## Preconditions

- User is logged into https://next.elitea.ai/app/
- A chat session is open with at least one skill participant added (e.g., "jira-skill")
- Skill participant is visible in PARTICIPANTS panel
- Skill is configured and functional

## Test Data

| Skill Participant | Test Message | Expected Response Indicators |
|-------------------|--------------|------------------------------|
| jira-skill | "List all projects in JIRA" | Streaming response, "Thought for X secs", skill badge, model badge |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Verify a skill participant (e.g., "jira-skill") is present in the PARTICIPANTS panel | Skill participant visible with version badge |
| 2 | Type a message in the chat input field addressing the skill (e.g., "List all projects in JIRA") | Message appears in the input field |
| 3 | Send the message by pressing Enter or clicking Send | Message is posted to the chat and appears in the message history |
| 4 | Observe the response from the skill participant | Response begins streaming in real-time (text appears progressively) |
| 5 | Verify "Thought for X secs" indicator appears during or before the response | "Thought for 3 secs" (or similar) is displayed, indicating processing time |
| 6 | Verify the skill badge is displayed with the response | Skill badge visible on the response message |
| 7 | Verify the model badge is displayed with the response | Model badge visible on the response message |
| 8 | Wait for the streaming response to complete | Full response is displayed, streaming stops, message is complete |
| 9 | Send a follow-up message to the same skill participant | Follow-up message is sent successfully and response streams again with the same indicators |

## Expected Final State

- Messages are successfully sent to skill participants
- Responses stream in real-time
- "Thought for X secs" indicator is displayed
- Skill badge and model badge are visible on responses
- Multiple messages can be exchanged in sequence

## Pass/Fail Criteria

**Pass:**
- Message is sent to skill participant successfully
- Response streams in real-time (text appears progressively)
- "Thought for X secs" indicator is displayed
- Skill badge is visible on response
- Model badge is visible on response
- Multiple messages can be sent and responded to in sequence

**Fail:**
- Message cannot be sent to skill participant
- Response does not stream (appears all at once or not at all)
- "Thought for X secs" indicator is missing
- Skill badge is missing or incorrect
- Model badge is missing or incorrect
- Follow-up messages fail to send or receive responses
