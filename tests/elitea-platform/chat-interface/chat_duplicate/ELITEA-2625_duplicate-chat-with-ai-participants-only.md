---
id: ELITEA-2625
title: "Duplicate Chat with AI Participants Only (Private Project)"
priority: medium
type: functional
module: chat-interface
status: ready
execution_type: manual
automation_test_id: []
tags: [chat, duplicate, ai-participants, private-project, P1]
requirements: [3837]
---
# ELITEA-2625: Duplicate Chat with AI Participants Only (Private Project)

**Module:** Chat Interface · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that duplicating a chat containing only AI participants (Agent/Pipeline/Toolkit/MCP) in a private project preserves all AI participants.

## Preconditions

- User is logged in to {{base_url}}
- Private project context (single user)
- Chat exists with AI participants: Agent, Pipeline, Toolkit, and/or MCP
- No user participants (private project limitation)

## Test Data

- URL: {{base_url}}
- Private project
- Original chat with: Agent, Pipeline, Toolkit, MCP

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to private project chat list | Private project label visible at top |
| 2 | Open a chat with AI participants only (Agent, Pipeline, Toolkit, MCP) | Chat opens with AI participants in panel |
| 3 | Note all AI participants and their types | Document: Agent name, Pipeline name, Toolkit name, MCP name |
| 4 | Duplicate the chat using context menu | Duplicate created successfully |
| 5 | Open the duplicated chat | Duplicated chat opens |
| 6 | Verify Agent participant is present | Agent participant copied with configuration |
| 7 | Verify Pipeline participant is present | Pipeline participant copied with configuration |
| 8 | Verify Toolkit participant is present | Toolkit participant copied |
| 9 | Verify MCP participant is present | MCP participant copied |
| 10 | Verify no user participants added automatically | Only AI participants present (single user owner) |

## Expected Final State

- Duplicated chat contains all AI participants from original
- Agent, Pipeline, Toolkit, MCP all preserved
- Participant configuration intact
- No unintended user participants added

## Pass/Fail Criteria

**Pass:**
- All AI participant types preserved (Agent/Pipeline/Toolkit/MCP)
- Participant configurations remain intact
- No additional participants added automatically
- Duplicate functions correctly with AI participants

**Fail:**
- Any AI participant missing
- Participant configuration lost
- Unintended participants added
- AI participants non-functional in duplicate
