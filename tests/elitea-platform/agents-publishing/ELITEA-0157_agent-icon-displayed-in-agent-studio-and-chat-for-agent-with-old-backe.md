---
id: ELITEA-0157
title: "Agent icon displayed in Agent Studio and Chat for agent with old backend response format"
priority: critical
type: functional
module: agents-publishing
status: draft
execution_type: manual
tags: [feat:agent-publishing, feat:agent-studio, r-2.0.2]
requirements: [EliteaAI/elitea_issues#4670]
---
# ELITEA-0157: Agent icon displayed in Agent Studio and Chat for agent with old backend response format

**Module:** Agents Publishing · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that an already-published agent whose backend response uses the old format (`icon_meta: { url, name }` only, no size fields) displays its correct icon in Agent Studio and in all Chat locations when opened via "Start Conversation".

**Coverage:**
- Icon rendering in Agent Studio for agents returned in old backend format
- Icon continuity when opening Chat via Start Conversation
- Icon in Chat agent list, agent popup, and next to agent messages
- Both icon types: predefined list icon and user-uploaded icon

## Preconditions

- Logged in to ELITEA
- Two existing published agents returned in the old backend response format (no `size`/`initial_file_size`/`resulting_file_size` in `icon_meta`):
  - One with a predefined list icon
  - One with a user-uploaded custom icon
- Navigate to Agent Studio

## Test Data

| # | Icon type | Example icon_meta |
|---|---|---|
| 1 | Predefined list icon | { "url": "https://.../default_entity_icons/image_0.png", "name": "image_0.png" } |
| 2 | User-uploaded icon | { "url": "https://.../application_icon/.../custom.png", "name": "custom.png" } — no size fields |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Agent Studio | Agent list is displayed |
| 2 | Find the published agent for this data variant (predefined icon / uploaded icon) | Agent card is visible with its assigned icon, not the fallback |
| 3 | Click Start Conversation on that agent | A new Chat opens with the agent pre-selected |
| 4 | Verify icon in the Chat agent list | Correct icon shown, not the fallback |
| 5 | Open the agent popup/details modal in Chat | Correct icon shown in the popup |
| 6 | Send a message to trigger an agent response | Agent responds; correct icon shown next to messages |

## Expected Final State

Agent responds; correct icon shown next to messages

## Pass/Fail Criteria

**Pass:**
- Correct icon shown in Agent Studio and in all Chat locations for both data variants

**Fail:**
- Fallback/generic icon shown at any step for either data variant
- One icon type works but the other does not
