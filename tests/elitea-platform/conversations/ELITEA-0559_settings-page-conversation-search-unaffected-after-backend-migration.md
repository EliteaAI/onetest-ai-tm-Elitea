---
id: ELITEA-0559
title: "Settings Page Conversation Search Unaffected After Backend Migration"
priority: high
type: functional
module: conversations
status: draft
execution_type: manual
tags: [eng:frontend, eng:backend, feat:chat, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4835]
---
# ELITEA-0559: Settings Page Conversation Search Unaffected After Backend Migration

**Module:** Conversations · **Priority:** High · **Type:** Functional

**Objective:** Verify that the Settings page conversation search — which already used backend search correctly — continues to work without regression after the main Chat page migration.

**Coverage:**
- Settings page sends query= parameter to backend when typing in search
- Matching conversations appear correctly in Settings search results
- No regression introduced by the Chat page refactoring

## Preconditions

- Logged in to {{base_url}} in the Private project
- Browser DevTools → Network tab open and recording
- At least one conversation exists with a known name

## Test Data

Search term: exact or partial name of an existing known conversation

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Settings from the sidebar | Settings page loads successfully |
| 2 | Locate the Conversations section in Settings | Conversations list is visible with a search input field |
| 3 | Type the name of a known conversation in the Settings search field | A GET request fires with query=<term> in the URL (confirm in DevTools) |
| 4 | Observe the search results | Matching conversation(s) appear in the Settings list |
| 5 | Click one of the results | Conversation opens or its details are accessible without error |

## Expected Final State

Conversation opens or its details are accessible without error

## Pass/Fail Criteria

**Pass:**
- Settings sends query=<term> to backend on typing
- Matching results appear correctly in Settings

**Fail:**
- Settings search no longer works or returns no results
- No query= parameter in the Settings request (regression introduced by Chat page migration)
