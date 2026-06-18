---
id: ELITEA-0153
title: "Chat — Active chat version unpublished (other versions exist): details/edit blocked, version switch resolves"
priority: critical
type: functional
module: agents-publishing
status: ready
execution_type: manual
tags: [feat:agent-publishing, r-2.0.2]
requirements: [EliteaAI/elitea_issues#4701]
---
# ELITEA-0153: Chat — Active chat version unpublished (other versions exist): details/edit blocked, version switch resolves

**Module:** Agents Publishing · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that when the version used in a chat is unpublished but other published versions of the same agent still exist — agent details/edit canvas cannot be opened from the chat, send is blocked on the unpublished version, but the user can switch to a working version after which the error disappears and the agent works correctly.

**Coverage:**
- Agent details / edit canvas cannot be opened from within the chat
- Agent CAN be selected in the chat participant picker
- Unpublished version is NOT available in the version selector
- Send is blocked while the unpublished version is active
- After switching to a published version: error notice disappears and send works

**Known Weak Point (current behavior, not yet fixed):**
- Sending a natural language message referencing the agent by name — without first switching versions — auto-selects the published version instead of blocking the request. This means the broken version is bypassed silently rather than surfacing an error.

## Preconditions

- Logged in to {{base_url}}
- Agent "Test Publishing" has at least 2 published versions (V1 and V2)
- Existing conversation was using V1
- V1 has been unpublished; V2 remains published

## Test Data

- Agent name: "Test Publishing"
- Unpublished version: V1
- Published version: V2
- Test message: "Hello"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the existing conversation that was using V1 (now unpublished). | Conversation view loads. Prior message history is visible. An error notice related to the unpublished version is shown in the chat. |
| 2 | Attempt to open agent details / edit canvas from within the chat (e.g., via the agent info icon, edit button, or any 'open details' control). | Agent details / edit canvas does not open. The action is blocked. |
| 3 | Attempt to select 'Test Publishing' via the chat participant picker. | Agent appears in the picker and can be selected. |
| 4 | Open the version selector for the agent. Check whether V1 (unpublished) is listed. | V1 is NOT available in the version selector. Only published versions (e.g., V2) are shown. |
| 5 | With V1 still active (no version switch yet), type "Hello" and attempt to send. | Send does not execute. No agent response is returned. |
| 6 | ⚠️ [Known Weak Point] Without switching versions, send a natural language message referencing the agent by name (e.g., "Run agent 'Test Publishing' with task: write a short story"). | Current behavior: the published version (V2) is auto-selected and the request executes. Note: this is a known weak point — the unpublished broken version is silently bypassed rather than surfacing an error. This behavior may change in a future fix. |
| 7 | Select V2 from the version selector. | Version changes to V2. The error notice in the conversation disappears. |
| 8 | Type "Hello" and send. | Message is sent successfully. Agent responds using V2. |

## Expected Final State

Message is sent successfully. Agent responds using V2.

## Pass/Fail Criteria

**Pass:**
- Agent details / edit canvas blocked from within chat
- Agent selectable in chat participant picker
- V1 (unpublished) absent from version selector
- Send blocked while unpublished version is active
- After switching to V2: error notice gone and send works

**Fail:**
- Agent details / edit canvas opens from within chat
- Unpublished V1 appears as selectable in the version selector
- Send works before version is switched
- Error persists after switching to V2
