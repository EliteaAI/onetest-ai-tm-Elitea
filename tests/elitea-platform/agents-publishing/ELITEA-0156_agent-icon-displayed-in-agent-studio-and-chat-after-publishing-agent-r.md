---
id: ELITEA-0156
title: "Agent icon displayed in Agent Studio and Chat after publishing agent returned in new backend response format"
priority: critical
type: functional
module: agents-publishing
status: draft
execution_type: manual
tags: [feat:agent-publishing, feat:agent-studio, r-2.0.2]
requirements: [EliteaAI/elitea_issues#4670]
---
# ELITEA-0156: Agent icon displayed in Agent Studio and Chat after publishing agent returned in new backend response format

**Module:** Agents Publishing · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that a newly published agent — whose backend response uses the new format (`icon_meta` includes `size`, `initial_file_size`, `resulting_file_size`) — displays its correct icon in Agent Studio immediately after publishing, and in all Chat locations via "Start Conversation".

**Coverage:**
- Publishing a new agent and verifying backend returns new response format with extended `icon_meta`
- Icon rendering in Agent Studio immediately after publish
- Icon continuity when opening Chat via Start Conversation
- Icon in Chat agent list, agent popup, and next to agent messages
- Both icon types: predefined list icon and user-uploaded icon

## Preconditions

- Logged in to ELITEA
- Agent Studio is accessible
- Ability to create and publish a new agent

## Test Data

| # | Icon type | Expected icon_meta after publish |
|---|---|---|
| 1 | Predefined list icon | { "url": "https://.../default_entity_icons/image_X.png", "name": "image_X.png", "size": "64x64", "initial_file_size": "...", "resulting_file_size": "..." } |
| 2 | User-uploaded custom icon | { "url": "https://.../application_icon/.../uuid.png", "name": "uuid.png", "size": "64x64", "initial_file_size": "...", "resulting_file_size": "..." } |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Agent Studio, create a new agent | Agent creation form opens |
| 2 | Set the icon for this data variant (select from predefined list / upload custom file) and fill required fields | Icon is selected/uploaded and saved |
| 3 | Publish the agent | Agent is published; API response contains new-format icon_meta with size and file size fields |
| 4 | Locate the newly published agent in Agent Studio | Agent card displays the assigned icon, not the fallback |
| 5 | Click Start Conversation on that agent | A new Chat opens with the agent pre-selected |
| 6 | Verify icon in the Chat agent list | Correct icon shown, not the fallback |
| 7 | Open the agent popup/details modal in Chat | Correct icon shown in the popup |
| 8 | Send a message to trigger an agent response | Agent responds; correct icon shown next to messages |

## Expected Final State

Agent responds; correct icon shown next to messages

## Pass/Fail Criteria

**Pass:**
- Icon correctly shown in Agent Studio immediately after publish for both data variants
- Same icon consistently shown in all Chat locations for both data variants

**Fail:**
- Fallback icon shown in Agent Studio after publishing (core bug scenario)
- Fallback icon shown in any Chat location
- One icon type works but the other does not
