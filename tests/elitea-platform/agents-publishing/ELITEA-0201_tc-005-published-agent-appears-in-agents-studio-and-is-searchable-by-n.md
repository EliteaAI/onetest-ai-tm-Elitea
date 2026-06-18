---
id: ELITEA-0201
title: "TC-005: Published Agent Appears in Agents Studio and Is Searchable by Name and Tag"
priority: critical
type: functional
module: agents-publishing
status: ready
execution_type: manual
tags: [feat:agents, story:3772, r-2.0.2]
requirements: [ProjectAlita/projectalita.github.io#3772]
---
# ELITEA-0201: TC-005: Published Agent Appears in Agents Studio and Is Searchable by Name and Tag

**Module:** Agents Publishing · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that after publishing an agent, it is immediately discoverable in Agents Studio by name search and by tag filter, and a new conversation can be started from Studio.

Coverage:
- Published agent discoverable via name search in Agents Studio
- Published agent discoverable via tag filter/category
- Agent card shows name, description, and author
- New conversation with published agent works end-to-end

## Preconditions

- Logged in as User A
- Agent C has been published with version 'v1.0' and at least 1 tag (e.g., 'Testing' or 'Development')

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Agents Studio (/agents-studio) | Agents Studio page loads with search bar and category filters |
| 2 | Type Agent C's exact name in the search box | Agent C's card appears in search results |
| 3 | Clear the search. Click the tag category that matches Agent C's tag | Agent C's card appears in the filtered results |
| 4 | Inspect Agent C's card in Studio | Card shows: agent name, description, author avatar |
| 5 | Click Agent C's card and select the published version | Agent detail or conversation start page opens |
| 6 | Start a new conversation with Agent C | Conversation starts; agent responds to a test prompt without error |

## Expected Final State

Conversation starts; agent responds to a test prompt without error

## Pass/Fail Criteria

PASS:
- Agent C is findable by name search in Studio immediately after publishing
- Agent C is findable by tag category filter
- Agent card displays correct name, description, and author
- New conversation with the published agent is functional

FAIL:
- Agent C does not appear in Agents Studio after publishing
- Name search or tag filter does not return Agent C
- Starting a conversation from Studio fails or errors
