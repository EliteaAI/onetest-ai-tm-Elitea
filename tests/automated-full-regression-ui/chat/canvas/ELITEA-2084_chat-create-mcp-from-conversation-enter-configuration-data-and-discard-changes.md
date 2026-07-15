---
id: ELITEA-2084
title: "Chat – Create MCP from Conversation – Enter Configuration Data and Discard Changes"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2084: Chat – Create MCP from Conversation – Enter Configuration Data and Discard Changes

**Module:** chat-interface · **Priority:** high · **Type:** functional

**Objective:** Verify that entering configuration data in the Create New MCP canvas and clicking Discard clears the data, and closing the canvas does not create an MCP entry in the PARTICIPANTS panel.

---

## Preconditions

- User is logged in to the Elitea platform.
- User has an open conversation in the Chats section.

---

## Test Data

| Field | Value |
|-------|-------|
| MCP Name | test |
| URL | https://api.githubcopilot.com/mcp |
| Client Secret | (any test value) |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Navigate to Chats and open a conversation | Conversation view is displayed |
| 2 | Click the + icon and select "MCPs" | MCPs submenu opens |
| 3 | Click "+ Create New MCP" at the top | "New MCP" canvas opens with "Choose the MCP type" section |
| 4 | Verify "Local" and "Remote" tabs are shown | Both tabs visible |
| 5 | Click the "Remote" tab and select "Remote MCP" | "New Remote MCP" configuration canvas opens |
| 6 | Type "test" in "Toolkit Name *" field | Name entered correctly |
| 7 | Type "https://api.githubcopilot.com/mcp" in "Url *" field | URL entered correctly |
| 8 | Enter a test value in "Client Secret" field | Secret value entered |
| 9 | Click the "Discard" button | Canvas clears all entered data |
| 10 | Verify the canvas remains open showing empty or default fields | Canvas is open but cleared |
| 11 | Click X to close the canvas | Canvas closes completely |
| 12 | Verify no "MCPS" section appears in the PARTICIPANTS panel and no MCP was created | No MCP entry in PARTICIPANTS |

---

## Expected Final State

Entered data is cleared after Discard; closing the canvas does not create an MCP. PARTICIPANTS panel shows no MCPS section.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Data is cleared; no MCP is created in the conversation.

**Fail:**
- Any step produces an error or unexpected result.
- MCP appears in PARTICIPANTS despite discarding.
