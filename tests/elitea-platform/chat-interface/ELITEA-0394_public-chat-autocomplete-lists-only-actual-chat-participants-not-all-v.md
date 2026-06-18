---
id: ELITEA-0394
title: "Public chat: autocomplete lists only actual chat participants, not all viewers"
priority: high
type: functional
module: chat-interface
status: ready
execution_type: manual
tags: [feat:chat, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4896]
---
# ELITEA-0394: Public chat: autocomplete lists only actual chat participants, not all viewers

**Module:** Chat Interface · **Priority:** High · **Type:** Functional

**Objective:** Verify that in a shared chat, the @mention autocomplete suggests only the users who were explicitly added to or have written in the chat — not all team members or viewers who simply have access to read the shared conversation.

**Coverage:**
- Autocomplete in a shared chat works and shows the actual participants
- Users who have view-only access to the shared chat (but were never added or wrote in it) are NOT listed in the autocomplete
- Partial-name filtering correctly applies to the limited participant scope
- Mention selection and message sending work correctly in a shared chat context

## Preconditions

- Logged into ELITEA at {{base_url}}
- A public chat exists in a team project that is visible to multiple team members (e.g., 5+ people have view access)
- Of those, only 2 have been explicitly added or sent messages in this chat: "Alice" (added participant) and "Bob" (wrote in the chat)
- A third team member "Carol" has view access to the shared chat but was never added and has never written in it
- Logged in as one of the 2 active participants

## Test Data

| Role | User | Active in chat? |
|---|---|---|
| Active participant (added) | "Alice" | Yes |
| Active participant (wrote) | "Bob" | Yes |
| Viewer only (has access, never added/wrote) | "Carol" | No |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the public chat | Chat view loads; participants panel shows only Alice and Bob — not Carol or other viewers |
| 2 | Click the message input and type `@` | Autocomplete dropdown appears |
| 3 | Inspect the dropdown entries | Only "Alice" and "Bob" are listed; "Carol" and other view-only users are absent |
| 4 | Type `C` after `@` (filtering for "Carol") | No suggestion for "Carol" appears; dropdown shows no match or empty state |
| 5 | Clear `C`; type `Al` to filter for Alice | Dropdown narrows to "Alice" only |
| 6 | Select "Alice"; complete and send the message | `@Alice` is inserted; message is sent and renders correctly in the shared chat |

## Expected Final State

`@Alice` is inserted; message is sent and renders correctly in the shared chat

## Pass/Fail Criteria

**Pass:**
- Dropdown lists only Alice and Bob (actual participants), not Carol or other view-only members
- Filtering for "Carol" yields no result
- Mention selection and send function correctly in the public chat

**Fail:**
- All team members with view access appear in the autocomplete suggestion list
- Dropdown is empty even though Alice and Bob are active participants
- Any error or unexpected behavior specific to the shared chat context
