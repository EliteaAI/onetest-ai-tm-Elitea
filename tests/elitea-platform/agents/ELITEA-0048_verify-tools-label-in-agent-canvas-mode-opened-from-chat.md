---
id: ELITEA-0048
title: "Verify \"TOOLS\" label in Agent canvas mode opened from Chat"
priority: high
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:agents, pipeline, 5117]
requirements: [EliteaAI/elitea_issues#5117]
---
# ELITEA-0048: Verify "TOOLS" label in Agent canvas mode opened from Chat

**Module:** Agents · **Priority:** High · **Type:** Functional

**Objective:** Verify that when an Agent is opened in canvas mode from Chat, the section label reads "TOOLS" (not "TOOLKITS").

**Coverage:**
- Label rename in canvas mode (Agent as Chat participant)

## Preconditions

- Logged in to {{base_url}}
- At least one Agent is added as a participant in a Chat conversation
- Browser: Chrome (latest)

## Test Data

Chat conversation with an Agent participant

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chat | Chat interface is displayed |
| 2 | Open a conversation that has an Agent as a participant | Conversation opens |
| 3 | Click on the Agent participant to open canvas/edit mode | Agent canvas panel opens on the right |
| 4 | Locate the tools section in the canvas panel | Section heading reads "TOOLS" |
| 5 | Confirm no "TOOLKITS" text is present | "TOOLKITS" is not visible |

## Expected Final State

"TOOLKITS" is not visible

## Pass/Fail Criteria

**Pass:** "TOOLS" label is shown; "TOOLKITS" is absent in canvas mode
**Fail:** "TOOLKITS" label appears or section heading is missing/blank
