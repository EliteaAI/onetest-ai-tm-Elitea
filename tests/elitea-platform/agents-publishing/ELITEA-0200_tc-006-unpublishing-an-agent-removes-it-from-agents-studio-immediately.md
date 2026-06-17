---
id: ELITEA-0200
title: "TC-006: Unpublishing an Agent Removes It From Agents Studio Immediately"
priority: critical
type: functional
module: agents-publishing
status: ready
execution_type: manual
tags: [feat:agents, story:3772, r-2.0.2]
requirements: [ProjectAlita/projectalita.github.io#3772]
---
# ELITEA-0200: TC-006: Unpublishing an Agent Removes It From Agents Studio Immediately

**Module:** Agents Publishing · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that when the owner unpublishes a published agent version, it is removed from Agents Studio immediately — it is not discoverable and cannot be used for new conversations.

Coverage:
- Unpublish option is available per published version
- Unpublish confirmation modal appears before action
- Agent removed from Studio listing after confirmation
- Agent not found via Studio search after unpublish
- Success notification shown after unpublish

## Preconditions

- Logged in as User A (owner of Agent C)
- Agent C is currently published and visible in Agents Studio

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Agent C in the project Agents list | Agent C detail page opens; published versions list is visible |
| 2 | Locate the 'Unpublish' option for version 'v1.0' | Unpublish option/button is visible per-version |
| 3 | Click 'Unpublish' on 'v1.0' | A confirmation modal opens |
| 4 | Verify the confirmation modal content | Modal shows: agent name, version being unpublished (v1.0), warning text about removal from Studio, notice about existing conversations |
| 5 | Click 'Confirm Unpublish' | Modal closes; success notification 'Agent unpublished successfully' (or equivalent) appears |
| 6 | Navigate to Agents Studio, search for Agent C by name | Agent C does NOT appear in search results |
| 7 | Browse Agents Studio category that Agent C was in | Agent C's card is not present |

## Expected Final State

Agent C's card is not present

## Pass/Fail Criteria

PASS:
- Unpublish confirmation modal shows all required content
- Agent C disappears from Agents Studio immediately after confirming unpublish
- Success notification is displayed
- Agent C is not findable via name or tag search in Studio

FAIL:
- No confirmation modal appears before unpublishing
- Agent C remains visible in Agents Studio after unpublish
- No success notification shown
- Agent C still appears in tag/category filter after unpublish
