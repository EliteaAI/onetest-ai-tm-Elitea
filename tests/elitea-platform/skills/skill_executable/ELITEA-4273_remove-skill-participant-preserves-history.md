---
id: ELITEA-4273
title: "Remove Skill Participant Preserves History"
priority: critical
type: functional
module: chat/skills
status: ready
execution_type: manual
tags: [user_story:6924, feat:skills, feat:chat-participants, skills-as-participants, message-history]
requirements: [EliteaAI/elitea_issues#6924]
---
# ELITEA-4273: Remove Skill Participant Preserves History

**Module:** Chat / Skills · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that removing a skill participant from the chat removes the participant from the PARTICIPANTS panel but preserves all message history with that skill in the chat.

## Preconditions

- User is logged into https://next.elitea.ai/app/
- A chat session is open with at least one skill participant added (e.g., "jira-skill")
- At least 2-3 messages have been exchanged with the skill participant (messages sent and responses received)
- Message history is visible in the chat

## Test Data

| Skill Participant | Messages Sent | Expected After Removal |
|-------------------|---------------|------------------------|
| jira-skill | "List projects", "Get project details", "Search issues" | All messages and responses remain visible in chat history |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Verify the skill participant (e.g., "jira-skill") is present in the PARTICIPANTS panel | Skill participant visible with version badge |
| 2 | Send at least 2-3 messages to the skill participant and receive responses | Messages and responses are visible in the chat history |
| 3 | Scroll through the chat to verify all messages are displayed | All sent messages and skill responses are visible in chronological order |
| 4 | Take note of the number of messages and responses in the chat history | Message count recorded for comparison |
| 5 | Locate the remove option for the skill participant in the PARTICIPANTS panel (e.g., "X" icon, "Remove" option, or context menu) | Remove option is visible and clickable |
| 6 | Click the remove option for the skill participant | Confirmation prompt may appear (if implemented) |
| 7 | Confirm the removal (if prompted) | Skill participant is removed from PARTICIPANTS panel |
| 8 | Verify the skill is no longer listed in the PARTICIPANTS panel | PARTICIPANTS panel does not show the removed skill |
| 9 | Scroll through the chat history and verify all previous messages and responses with the removed skill are still visible | All messages and responses remain in the chat history, no messages are deleted |
| 10 | Verify the message count matches the count from step 4 (no messages removed) | Message count is unchanged |
| 11 | Verify the removed skill participant cannot receive new messages (optional check: attempt to send a message to the removed skill) | Removed skill does not respond or is not addressable (UI may prevent sending) |

## Expected Final State

- Skill participant is removed from PARTICIPANTS panel
- All message history with the removed skill remains visible in the chat
- No messages or responses are deleted from the chat history
- Removed skill participant cannot receive new messages

## Pass/Fail Criteria

**Pass:**
- Skill participant is successfully removed from PARTICIPANTS panel
- All messages sent to the skill before removal remain visible in chat history
- All responses from the skill before removal remain visible in chat history
- Message count and order are unchanged after removal
- Removed skill cannot receive new messages

**Fail:**
- Skill participant is not removed from PARTICIPANTS panel
- Any messages or responses are deleted from chat history
- Message count decreases after removal
- Chat history is corrupted or reordered
- Removed skill can still receive new messages
