---
id: ELITEA-3930
title: "Duplicated Chat Preserves All Participants and Configuration"
priority: high
type: functional
module: chat-interface
status: ready
execution_type: manual
tags: [chat, duplicate, participants, P0]
requirements: [3837]
---
# ELITEA-3930: Duplicated Chat Preserves All Participants and Configuration

**Module:** Chat Interface · **Priority:** High · **Type:** Functional

**Objective:** Verify that opening a duplicated chat shows all participants and chat configuration preserved from the original chat.

## Preconditions

- User is logged in to {{base_url}}
- An existing chat with multiple participants (users and/or AI) exists
- Chat has specific configuration settings

## Test Data

- URL: {{base_url}}
- Original chat with:
  - Multiple user participants (in team project)
  - AI participants (Agent/Pipeline/Toolkit/MCP)
  - Specific chat settings

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open an existing chat and note all participants in the Participants panel | Original chat shows all participants (Users, Agents, Pipelines, Toolkits, MCPs) |
| 2 | Note any specific chat configuration or settings | Chat configuration is documented |
| 3 | Duplicate the chat using the context menu | Duplicate action completes successfully |
| 4 | Open the newly duplicated chat | Duplicated chat opens |
| 5 | Open the Participants panel in the duplicated chat | Participants panel displays |
| 6 | Verify all user participants from the original chat are present | All user participants are copied (Bug #6256 validation) |
| 7 | Verify all AI participants (Agent/Pipeline/Toolkit/MCP) are present | All AI participants are copied with their configuration |
| 8 | Verify chat configuration matches the original | Chat settings are preserved |

## Expected Final State

- Duplicated chat contains all participants from original
- All participant types (Users, Agents, Pipelines, Toolkits, MCPs) are preserved
- Chat configuration matches the original
- No messages are copied (empty conversation)

## Pass/Fail Criteria

**Pass:**
- All user participants are present in duplicated chat
- All AI participants are present with correct configuration
- Chat settings match the original
- Conversation history is empty

**Fail:**
- Any participant is missing (especially Bug #6256: only creator copied)
- AI participants lose configuration
- Chat settings are different
- Messages are copied to duplicate
