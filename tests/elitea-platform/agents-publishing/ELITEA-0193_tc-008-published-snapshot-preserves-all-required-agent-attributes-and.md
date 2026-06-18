---
id: ELITEA-0193
title: "TC-008: Published Snapshot Preserves All Required Agent Attributes and Remains Frozen After Source Edit"
priority: high
type: functional
module: agents-publishing
status: draft
execution_type: manual
tags: [feat:agents, story:3772, r-2.0.2]
requirements: [ProjectAlita/projectalita.github.io#3772]
---
# ELITEA-0193: TC-008: Published Snapshot Preserves All Required Agent Attributes and Remains Frozen After Source Edit

**Module:** Agents Publishing · **Priority:** High · **Type:** Functional

**Objective:** Verify that the published agent snapshot in Agents Studio faithfully contains all required attributes and is immutable — editing the source agent after publish does not change the already-published version.

Coverage:
- Name, description, icon, tags, welcome message, conversation starters, variables, internal tools all present in snapshot
- Each attribute matches the original at time of publish
- Snapshot does not change when source agent is subsequently edited

## Preconditions

- Logged in as User A
- Agent A is fully configured with all attributes
- Agent A published with version 'v1.0-snap-test'
- Record before publishing: agent name, description, icon (custom/non-default), tags, welcome message, conversation starters, variable name + default value, enabled internal tool

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Record all Agent A attributes (name, description, icon, tags, welcome message, conversation starters, variable + default value, enabled internal tool) | All values documented |
| 2 | Publish Agent A with version 'v1.0-snap-test' | Publish succeeds |
| 3 | In Agents Studio, open Agent A's published version and verify description matches original | Description text is identical to what was recorded |
| 4 | Verify icon matches (non-default) | Custom icon is displayed, not the platform default |
| 5 | Verify tags are present | All recorded tags are visible on the agent card or filter |
| 6 | Start a conversation with the published agent and verify welcome message appears at start | Welcome message matches recorded text |
| 7 | Verify conversation starters are displayed | All 2+ starters are visible |
| 8 | Ask the agent to use its enabled internal tool | Tool executes correctly in the conversation |
| 9 | Go back to source Agent A. Change the description to something different and save. | Source agent description updated |
| 10 | Return to Agents Studio, view Agent A's 'v1.0-snap-test' | Description in Studio still shows the original published description (unchanged) |

## Expected Final State

Description in Studio still shows the original published description (unchanged)

## Pass/Fail Criteria

PASS:
- All attributes in the published snapshot match what was configured at publish time
- Editing the source agent after publish does not alter the published snapshot

FAIL:
- Any attribute is missing or incorrect in the published snapshot
- The published snapshot reflects post-publish edits to the source agent (not frozen)
- Internal tool fails to execute in the published agent conversation
