---
id: ELITEA-0409
title: "Sending Message With `/` Mention Does Not Add or Remove Participants"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [user_story:2925, feat:chat, r-2.0.3]
requirements: [EliteaAI/elitea_issues#2925]
---
# ELITEA-0409: Sending Message With `/` Mention Does Not Add or Remove Participants

**Module:** Chat Interface · **Priority:** High · **Type:** Functional

**Objective:** Verify the Participants list is not modified when a message containing a `/` mention is sent.

**Coverage:**
- Participants panel unchanged after sending message with mention
- No new toolkit/MCP auto-added

## Preconditions

- Artifacts toolkit in Participants; no other toolkits/MCPs

## Test Data

- Mention: /Artifacts/create_file
- Full message: /Artifacts/create_file test.txt with some content

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open chat conversation with only Artifacts in Participants. Note current state. | Participants: Toolkits = Artifacts only. |
| 2 | Type /, select Artifacts, select create_file. Append text  test.txt. | Input shows /Artifacts/create_file test.txt. |
| 3 | Click Send. | Message is sent. |
| 4 | After response is received, inspect the Participants panel. | Toolkits section still shows only Artifacts. |
| 5 | Verify no MCPs or new toolkits were added. | No changes to Participants list. |

## Expected Final State

No changes to Participants list.

## Pass/Fail Criteria

**Pass:**
- Participants list identical before and after sending
- No auto-added participants

**Fail:**
- New toolkit or MCP appears in Participants after sending
- Any existing participant is removed
