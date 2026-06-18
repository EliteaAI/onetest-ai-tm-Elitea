---
id: ELITEA-0109
title: "Agent/Pipeline header stays fixed while scrolling through configuration"
priority: high
type: functional
module: agents
status: ready
execution_type: manual
tags: [nfr:usability, eng:frontend, feat:agents, issue:3707, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3707]
---
# ELITEA-0109: Agent/Pipeline header stays fixed while scrolling through configuration

**Module:** Agents · **Priority:** High · **Type:** Functional

**Objective:** Verify that the header displaying the agent/pipeline name remains fixed (sticky) at the top of the page when the user scrolls through the configuration content.

**Coverage:**
- Header stickiness when scrolling past Instructions, Toolkits, Welcome Message sections
- Same sticky behavior on both Agent and Pipeline detail pages

## Preconditions

- Logged in to {{base_url}} with a valid user account
- An Agent and a Pipeline with substantial configuration content (long instructions, multiple toolkits) to require scrolling

## Test Data

- Agent with a long system prompt and multiple toolkits configured
- Pipeline with multiple nodes or states configured

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the Agent/Pipeline page. Open an agent/pipeline with a long configuration (long instructions, multiple toolkits). | Agent/Pipeline detail page opens with the name visible in the header. |
| 2 | Scroll down slowly through the GENERAL, INSTRUCTIONS, WELCOME MESSAGE, and TOOLKITS sections. | The header (containing the entity name, VERSION selector, Save/Discard buttons) remains fixed at the top and does not scroll out of view. |
| 3 | Scroll back to the top. | Page returns to the top; header still shows the correct name. |

## Expected Final State

Page returns to the top; header still shows the correct name.

## Pass/Fail Criteria

**Pass:**
- Agent/pipeline name header stays visible and fixed at the top throughout scrolling

**Fail:**
- Header scrolls out of view when scrolling down the configuration page for either entity type
