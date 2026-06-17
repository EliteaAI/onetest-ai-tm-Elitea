---
id: ELITEA-0055
title: "Verify TOOLS section collapse/expand in Agent canvas mode from Chat"
priority: high
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:agents, pipeline, 5117]
requirements: [EliteaAI/elitea_issues#5117]
---
# ELITEA-0055: Verify TOOLS section collapse/expand in Agent canvas mode from Chat

**Module:** Agents · **Priority:** High · **Type:** Functional

**Objective:** Verify that the TOOLS section can be collapsed and expanded when an Agent is open in canvas mode from Chat.

**Coverage:**
- Collapse/expand toggle behavior in Agent canvas mode

## Preconditions

- Logged in to {{base_url}}
- A Chat conversation has an Agent as participant
- Agent canvas panel is open
- Browser: Chrome (latest)

## Test Data

Chat conversation with an Agent participant that has at least one tool configured

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Chat and click the Agent participant to open canvas mode | Agent canvas panel is displayed |
| 2 | Confirm TOOLS section is visible and expanded | TOOLS section content (buttons and tools) is visible |
| 3 | Click the collapse toggle (>) next to TOOLS | TOOLS section collapses; content is hidden; "TOOLS" label remains |
| 4 | Click the expand toggle (v) next to TOOLS | TOOLS section expands; all content is restored |
| 5 | Verify buttons and tools are visible after expand | + Toolkit, + MCP, + Agent, + Pipeline buttons and configured tools are shown |

## Expected Final State

+ Toolkit, + MCP, + Agent, + Pipeline buttons and configured tools are shown

## Pass/Fail Criteria

**Pass:** Collapse and expand work correctly; \"TOOLS\" label persists in both states
**Fail:** Toggle does not work, content is lost, or label disappears
