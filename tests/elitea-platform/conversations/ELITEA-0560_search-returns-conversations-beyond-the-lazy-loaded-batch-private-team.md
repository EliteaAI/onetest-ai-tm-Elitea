---
id: ELITEA-0560
title: "Search Returns Conversations Beyond the Lazy-Loaded Batch [Private & Team]"
priority: critical
type: functional
module: conversations
status: draft
execution_type: manual
tags: [eng:frontend, eng:backend, feat:chat, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4835]
---
# ELITEA-0560: Search Returns Conversations Beyond the Lazy-Loaded Batch [Private & Team]

**Module:** Conversations · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that backend search finds conversations that were not yet fetched by lazy loading — the full backend dataset is searched, not just the frontend cache.

**Coverage:**
- Private project: search returns a conversation that is NOT in the first lazy-loaded batch
- Team project: search returns a team conversation that is NOT in the first lazy-loaded batch
- Conversation opens correctly when clicked from search results

## Preconditions

- Logged in to {{base_url}}
- Private project has more conversations than the batch size (>15), with at least one conversation in the "Older" group that is NOT in the first loaded batch
- Team project has same condition
- Record the exact name of the target conversations before testing

## Test Data

| # | Project type | Target conversation |
|---|---|---|
| 1 | Private | A conversation from >1 month ago, not visible in the first loaded batch |
| 2 | Team | A team conversation not rendered in the first lazy-loaded batch |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Chat in the Private project and wait for the first batch to load | Only the first batch of conversations is rendered; the target old conversation is NOT visible |
| 2 | Click the search icon and type the exact name of the target conversation | Backend GET request fires with query=<name>; search results appear |
| 3 | Check if the target conversation appears in the search results | The target conversation is visible in search results despite not being in the pre-loaded batch |
| 4 | Click the conversation from search results | Conversation opens correctly in the main chat area without errors |
| 5 | Switch to a Team project and repeat steps 1–4 for a team conversation not in the first batch | Same result: conversation found via backend search even though it was not yet lazy-loaded |

## Expected Final State

Same result: conversation found via backend search even though it was not yet lazy-loaded

## Pass/Fail Criteria

**Pass:**
- Target conversation appears in search results in both project types
- Conversation was confirmed absent from the pre-loaded list before search
- Clicking the result opens the conversation without error

**Fail:**
- Conversation does not appear in search results (only loaded conversations are searchable)
- An error or empty state appears despite matching conversations existing
