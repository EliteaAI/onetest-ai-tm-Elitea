---
id: ELITEA-0564
title: "Backend Search API Is Triggered When Typing in Search Box [Private & Team]"
priority: critical
type: functional
module: conversations
status: draft
execution_type: manual
tags: [eng:frontend, eng:backend, feat:chat, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4835]
---
# ELITEA-0564: Backend Search API Is Triggered When Typing in Search Box [Private & Team]

**Module:** Conversations · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that typing in the Chat sidebar search field triggers a backend API call with a `query=` parameter in both Private and Team projects — replacing client-side filtering.

**Coverage:**
- Private project: typing in search sends GET request with `query=` parameter to backend
- Team project: typing in search sends GET request with `query=` parameter to backend
- Request does NOT use `limit=1000` (old workaround removed)
- No cross-project conversation bleed in Team project results

## Preconditions

- Logged in to {{base_url}}
- Browser DevTools → Network tab is open and recording
- Access to at least one Private project and one Team project with existing conversations

## Test Data

| # | Project type | Search term |
|---|---|---|
| 1 | Private | test |
| 2 | Team | test |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chat page in the Private project | Chat sidebar shows Conversations list with date groups |
| 2 | Click the magnifying glass (Search conversations) icon in the sidebar | Search input field appears and is focused |
| 3 | Type 'test' in the search field | Characters are entered in the field |
| 4 | Inspect outgoing network requests in DevTools | A GET request is fired to /api/v2/elitea_core/folder/prompt_lib/{id} or /conversations/prompt_lib/{id} with query=test in the URL parameters |
| 5 | Check the limit parameter in the network request | The limit parameter is ≤100 (batch size), NOT 1000 |
| 6 | Switch to a Team project using the project switcher | Team project Chat page loads |
| 7 | Repeat steps 2–5 for the Team project | GET request includes query=test, no limit=1000, and no Private project conversations appear in Team results |

## Expected Final State

GET request includes query=test, no limit=1000, and no Private project conversations appear in Team results

## Pass/Fail Criteria

**Pass:**
- Both Private and Team projects send a GET request with `query=test` to the backend on typing
- Neither request uses `limit=1000`
- Team project results contain only Team conversations (no cross-project bleed)

**Fail:**
- No backend request with `query=` is fired (search remains client-side only)
- Request uses `limit=1000`
- Team results include conversations from the Private project
