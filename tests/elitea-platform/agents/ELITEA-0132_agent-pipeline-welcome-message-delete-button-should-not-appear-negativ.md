---
id: ELITEA-0132
title: "Agent/Pipeline - Welcome Message Delete Button Should Not Appear (Negative Test)"
priority: high
type: functional
module: agents
status: draft
execution_type: manual
tags: []
requirements: []
---
# ELITEA-0132: Agent/Pipeline - Welcome Message Delete Button Should Not Appear (Negative Test)

**Module:** Agents · **Priority:** High · **Type:** Functional

**Objective:** Verify that the Delete button does not appear on welcome message blocks in agent and pipeline chats. If it does appear, clicking it should not cause a server error.

## Preconditions

User logged into Elitea stage.elitea.ai\nAgent with a welcome message configured exists\nPipeline with a welcome message configured exists

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to an agent detail page that has a welcome message configured | Agent detail page loads with embedded chat panel showing welcome message |
| 2 | Hover over the welcome message block in the chat | No Delete button (aria-label='Delete') should appear on the welcome message |
| 3 | If Delete button IS visible, click it | No 500 Internal Server Error; either action is gracefully rejected or button should not exist |
| 4 | Open browser DevTools Network tab and check for any 500 responses | No 500 error responses in network traffic |
| 5 | Repeat steps 1-4 for a pipeline with welcome message configured | Same behavior: Delete button absent on pipeline welcome message |
| 6 | Verify that regular chat messages (non-welcome) still show the Delete button | Delete button appears normally on user/AI messages that are not welcome messages |

## Expected Final State

Delete button appears normally on user/AI messages that are not welcome messages

## Pass/Fail Criteria

Delete button NOT visible on welcome message blocks\nNo 500 Internal Server Error in any scenario\nPage remains responsive\nRegular message Delete button still functional
