---
id: ELITEA-0509
title: "\"Allow attachments\" toggle in Agent configuration enables and disables the paperclip icon"
priority: high
type: functional
module: chat-attachments
status: ready
execution_type: manual
tags: [feat:attachments, issue:1285, feat:chat, r-2.0.0b]
requirements: [ProjectAlita/projectalita.github.io#1285]
---
# ELITEA-0509: "Allow attachments" toggle in Agent configuration enables and disables the paperclip icon

**Module:** Chat Attachments · **Priority:** High · **Type:** Functional

**Objective:** Verify that the "Allow attachments" toggle in the Agent configuration INTERNAL TOOLS section controls whether the paperclip icon is active in chat conversations using that agent — and that disabling it deactivates attachments in new conversations.

**Coverage:**
- Toggle OFF (default): paperclip is disabled in Agent conversations
- Toggle ON + Save: paperclip becomes active in Agent conversations
- File attaches and is processed correctly after enabling
- Toggle OFF + Save: paperclip disabled again in new conversations
- Editor/Admin permissions required for toggle — not Viewer

## Preconditions

- Logged into ELITEA at {{base_url}} with Editor or Admin role
- An existing Agent available for configuration

## Test Data

- Agent name: any existing agent (e.g., test-agent)
- Test file: `sample.png` (~500 KB)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Agents → open any agent → Configuration tab → locate INTERNAL TOOLS section | "Allow attachments" toggle is visible; it is OFF by default |
| 2 | Start a conversation with this agent (toggle is still OFF) | Paperclip icon in the chat input area is disabled/greyed out; clicking it has no effect |
| 3 | Return to Agent Configuration → set "Allow attachments" toggle to ON → click Save | Agent saved successfully; toggle state persists as ON after save |
| 4 | Open a new conversation with this agent | Paperclip icon is now enabled and clickable |
| 5 | Click the paperclip → attach `sample.png` → type "Describe this image" → Send | File attaches successfully; AI processes and describes the image |
| 6 | Return to Agent Configuration → set "Allow attachments" toggle to OFF → Save | Agent saved; in a new conversation with this agent, the paperclip is disabled again |

## Expected Final State

Agent saved; in a new conversation with this agent, the paperclip is disabled again

## Pass/Fail Criteria

**Pass:**
- Toggle OFF → paperclip disabled in agent conversations
- Toggle ON + Save → paperclip enabled; file attaches and AI processes it
- Toggle OFF again → paperclip disabled in subsequent conversations

**Fail:**
- Toggle has no effect on paperclip state
- Paperclip accessible when toggle is OFF
- Toggle state not persisted after save
