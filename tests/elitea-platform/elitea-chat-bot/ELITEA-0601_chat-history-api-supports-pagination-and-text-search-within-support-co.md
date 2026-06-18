---
id: ELITEA-0601
title: "Chat history API supports pagination and text search within support conversations"
priority: medium
type: functional
module: elitea-chat-bot
status: ready
execution_type: manual
tags: [history-api, story:4781, pagination, r-2.0.3, search]
requirements: [4781]
---
# ELITEA-0601: Chat history API supports pagination and text search within support conversations

**Module:** Elitea Chat Bot · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that the support chat history listing endpoint supports pagination (limit/offset or page parameters) and text search filtering. Pagination ensures the UI can handle users with many past sessions without loading everything at once. Search enables the history search feature in the UI.

## Preconditions

User has at least 5 past support conversations (create them if needed).
API client available with authenticated token.

## Test Data

5+ support conversations for the test user
Search keyword: a word known to appear in one of the conversation names/messages

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Send GET /v2/support_assistant/conversations?limit=2&offset=0 | HTTP 200; response contains exactly 2 conversations |
| 2 | Send GET /v2/support_assistant/conversations?limit=2&offset=2 | HTTP 200; response contains the next 2 conversations (different from step 1) |
| 3 | Send GET /v2/support_assistant/conversations?search=<keyword> where keyword is known to match one conversation | HTTP 200; response contains only conversations matching the keyword |
| 4 | Send GET /v2/support_assistant/conversations?search=zzz_no_match_xyz | HTTP 200; response is an empty array (no results) — not a 404 or error |

## Expected Final State

HTTP 200; response is an empty array (no results) — not a 404 or error

## Pass/Fail Criteria

PASS: Pagination returns correct counts; search returns matching results; no-match returns empty array.
FAIL: Pagination not supported (all conversations returned regardless of limit); search not supported or returns errors; no-match returns 404.
