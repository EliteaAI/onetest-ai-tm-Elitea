---
id: ELITEA-3768
title: "Export Conversation With AI Agent Participant"
priority: high
type: functional
module: conversations
status: ready
execution_type: manual
tags: [eng:frontend, eng:backend, feat:chat, feat:export, feat:agents, r-2.0.8]
requirements: [EliteaAI/elitea_issues#4590]
---
# ELITEA-3768: Export Conversation With AI Agent Participant

**Module:** Conversations · **Priority:** High · **Type:** Functional

**Objective:** Verify that conversations involving AI agents (custom agents, pipelines, etc.) export correctly with AI participant metadata.

**Coverage:**
- Conversations with AI agent participants can be exported
- AI agent messages included in export
- AI agent metadata properly identified in JSON
- Message chronology maintained between user and AI agent

## Preconditions

- Logged in to {{base_url}}
- Conversation exists with at least one AI agent participant (Agent, Pipeline, etc.)
- User is the conversation creator

## Test Data

- Conversation with messages from: User + AI Agent (or Pipeline)
- At least 5 messages exchanged between user and AI agent

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chats section | Chat list displays |
| 2 | Identify conversation with AI agent participant | Verify Participants panel shows AI agent (e.g., agent icon/label) |
| 3 | Right-click conversation | Context menu with "Export" appears |
| 4 | Click "Export" | Dialog opens |
| 5 | Select export option (with or without attachments) | Selection made |
| 6 | Click "Export" | File downloads (JSON or ZIP) |
| 7 | Extract and open JSON file | JSON structure visible |
| 8 | Verify messages from AI agent included | AI agent messages present in messages array |
| 9 | Verify AI agent metadata in JSON - Sender type | Sender field indicates AI/agent, e.g., "type": "agent" or "type": "pipeline" |
| 10 | Verify AI agent metadata in JSON - Agent name | Agent name/identifier included in sender metadata |
| 11 | Verify AI agent metadata in JSON - Timestamps | AI-generated messages have timestamps |
| 12 | Verify message order includes both user and AI | Chronological order maintained (user messages + AI messages interleaved correctly) |
| 13 | If AI agent generated artifacts/attachments | Verify artifacts included in ZIP if "With attachments" selected |
| 14 | Verify participant list in JSON metadata | JSON includes participant info showing AI agent type |

## Expected Final State

- JSON file contains all messages from both user and AI agent
- AI agent metadata clearly indicates agent type and name
- Message chronology correct
- Success notification displayed

## Pass/Fail Criteria

**Pass:**
- All AI agent messages exported in JSON
- Metadata indicates agent type (agent/pipeline)
- Agent name/identifier present
- Chronological order maintained
- AI-generated attachments included if selected

**Fail:**
- AI agent messages missing or incomplete
- No indication of sender type (AI vs human)
- Agent metadata missing or incorrect
- Message order broken
- Attachments from AI agent missing

## Postconditions

- Original conversation unchanged
- AI agent remains functional in conversation
