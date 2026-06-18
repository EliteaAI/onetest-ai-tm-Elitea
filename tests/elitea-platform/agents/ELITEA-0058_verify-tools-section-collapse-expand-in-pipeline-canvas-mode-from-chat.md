---
id: ELITEA-0058
title: "Verify TOOLS section collapse/expand in Pipeline canvas mode from Chat"
priority: high
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:agents, pipeline, 5117]
requirements: [EliteaAI/elitea_issues#5117]
---
# ELITEA-0058: Verify TOOLS section collapse/expand in Pipeline canvas mode from Chat

**Module:** Agents · **Priority:** High · **Type:** Functional

**Objective:** Verify that the TOOLS section can be collapsed and expanded when a Pipeline is open in canvas mode from Chat.

**Coverage:**
- Collapse/expand toggle behavior in Pipeline canvas mode

## Preconditions

- Logged in to {{base_url}}
- A Chat conversation has a Pipeline as participant
- Pipeline canvas panel is open
- Browser: Chrome (latest)

## Test Data

Chat conversation with a Pipeline participant that has at least one tool configured

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Chat and click the Pipeline participant to open canvas mode | Pipeline canvas panel is displayed |
| 2 | Confirm TOOLS section is visible and expanded | TOOLS section content (buttons and tools) is visible |
| 3 | Click the collapse toggle (>) next to TOOLS | TOOLS section collapses; content is hidden; "TOOLS" label remains |
| 4 | Click the expand toggle (v) next to TOOLS | TOOLS section expands; all content is restored |
| 5 | Verify buttons and tools are visible after expand | All 4 buttons and configured tools are shown |

## Expected Final State

All 4 buttons and configured tools are shown

## Pass/Fail Criteria

**Pass:** Collapse and expand work correctly; \"TOOLS\" label persists in both states
**Fail:** Toggle does not work, content is lost, or label disappears
