---
id: ELITEA-0561
title: "Clearing Search Field Restores Normal Lazy-Loading Conversation List"
priority: critical
type: functional
module: conversations
status: draft
execution_type: manual
tags: [eng:frontend, eng:backend, feat:chat, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4835]
---
# ELITEA-0561: Clearing Search Field Restores Normal Lazy-Loading Conversation List

**Module:** Conversations · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that clearing the search input stops backend search calls and restores the sidebar to the normal paginated conversation list with correct date groups and working lazy loading.

**Coverage:**
- Clearing search field stops search API calls
- Normal date-grouped conversation list is restored
- Lazy loading (scroll-triggered pagination) resumes correctly after clearing search
- No missing conversations or duplicate entries in the restored list

## Preconditions

- Logged in to {{base_url}} in the Private project
- Browser DevTools → Network tab open and recording
- More conversations than the batch size are present

## Test Data

Search term: test

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the Chat page, activate search and type 'test' | Backend GET with query=test fires; search results appear in sidebar |
| 2 | Clear the search field completely (backspace all characters or click the clear button) | Search field is empty |
| 3 | Observe the sidebar | Conversation list returns to normal view with date groups: Pinned / Today / This Week / Older |
| 4 | Check DevTools for new network requests | No new query= API calls fire after clearing; only standard pagination requests are present |
| 5 | Scroll down slowly in the conversation list | A new GET request fires with incremented offset and no query parameter (lazy loading resumed) |
| 6 | Inspect the full sidebar conversation list | No conversations are missing and no duplicate entries are present; date grouping is correct |

## Expected Final State

No conversations are missing and no duplicate entries are present; date grouping is correct

## Pass/Fail Criteria

**Pass:**
- Sidebar returns to normal date-group view after clearing search
- No search API calls fire after clearing
- Lazy loading (scroll-triggered pagination) resumes correctly
- No missing or duplicate conversations

**Fail:**
- Search results remain visible after clearing
- Lazy loading does not work after clearing search
- Conversations are missing or duplicated in the restored list
