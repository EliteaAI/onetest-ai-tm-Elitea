---
id: ELITEA-0190
title: "TC-011: Sub-Agents Embedded in Snapshot Are Not Listed Separately in Agents Studio"
priority: high
type: functional
module: agents-publishing
status: draft
execution_type: manual
tags: [feat:agents, story:3772, r-2.0.2]
requirements: [ProjectAlita/projectalita.github.io#3772]
---
# ELITEA-0190: TC-011: Sub-Agents Embedded in Snapshot Are Not Listed Separately in Agents Studio

**Module:** Agents Publishing · **Priority:** High · **Type:** Functional

**Objective:** Verify that sub-agents embedded within a published agent are bundled into the parent agent snapshot and do not appear as standalone agents in Agents Studio, while still being callable internally by the parent agent.

Coverage:
- Sub-agent name not visible as a standalone listing in Agents Studio
- Sub-agent not findable via Studio name search
- Sub-agent is still internally invokable by the parent agent during a conversation

## Preconditions

- Logged in as User A
- Agent B has a sub-agent (e.g., "Code Helper Sub-Agent")
- Agent B has been published with version 'v1.0'

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Note the exact name of the sub-agent inside Agent B | Sub-agent name recorded |
| 2 | Navigate to Agents Studio and search for the sub-agent's exact name | No results for the sub-agent name appear |
| 3 | Browse all Studio categories | Sub-agent is not visible as a standalone card in any category |
| 4 | Start a conversation with published Agent B from Studio | Conversation starts |
| 5 | Send a prompt that requires the parent agent to invoke the sub-agent | Parent agent invokes sub-agent internally and returns a result; sub-agent's work is visible in the response |

## Expected Final State

Parent agent invokes sub-agent internally and returns a result; sub-agent's work is visible in the response

## Pass/Fail Criteria

PASS:
- Sub-agent does not appear as a standalone listing in Agents Studio
- Sub-agent is not found by Studio name search
- Sub-agent is still callable internally by the parent agent in a conversation

FAIL:
- Sub-agent appears as a standalone card in Agents Studio
- Sub-agent is invokable directly by Studio users independently
