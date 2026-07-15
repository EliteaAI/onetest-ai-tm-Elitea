---
id: ELITEA-2094
title: "Chat – Create New Conversation with Agent, Toolkit, MCP, and Pipeline – Verify All Participants Are Added and Displayed Correctly"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2094: Chat – Create New Conversation with Agent, Toolkit, MCP, and Pipeline – Verify All Participants Are Added and Displayed Correctly

**Module:** chat-interface · **Priority:** high · **Type:** functional

**Objective:** Verify that adding an Agent, Pipeline, Toolkit, and MCP to a new conversation via the + menu correctly populates all four sections in the PARTICIPANTS panel with distinct icons, and that sending a message shows the owner in PARTICIPANTS.

---

## Preconditions

- User is logged in to the Elitea platform.
- Available agents, pipelines, toolkits, and MCPs exist in the project.

---

## Test Data

| Field | Value |
|-------|-------|
| First message | Hi |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Navigate to Chats and click "+ Chat" | New conversation created; PARTICIPANTS panel empty |
| 2 | Click + icon, click "Agents", select an agent from the list | Agent appears in AGENTS section of PARTICIPANTS |
| 3 | Click + icon, click "Pipelines", select a pipeline from the list | Pipeline appears in PIPELINES section of PARTICIPANTS |
| 4 | Click + icon, click "Toolkits", enable a toolkit via toggle | Toolkit appears in TOOLKITS section of PARTICIPANTS |
| 5 | Click + icon, click "MCPs", enable an MCP via toggle | MCP appears in MCPS section of PARTICIPANTS |
| 6 | Verify all four sections are visible in PARTICIPANTS: AGENTS, PIPELINES, TOOLKITS, MCPS | All four sections displayed with respective participants |
| 7 | Verify each participant has a distinct icon (robot for agent, flowchart for pipeline, wrench for toolkit, plugin for MCP) | Icons are distinct and correct |
| 8 | Verify no duplicate entries for any participant | No duplicates present |
| 9 | Type "Hi" and click Send | Conversation is created; owner icon added to PARTICIPANTS |
| 10 | Verify all participants are visible under their type sections | All participants remain listed |
| 11 | Verify misconfigured entities show yellow warning messages | Warnings shown for misconfigured items |

---

## Expected Final State

All four participant types are added and displayed correctly in the PARTICIPANTS panel with distinct icons. After sending the first message, the owner also appears.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- All four participant types display correctly with distinct icons.

**Fail:**
- Any step produces an error or unexpected result.
- A participant type is missing, duplicated, or shows wrong icons.
