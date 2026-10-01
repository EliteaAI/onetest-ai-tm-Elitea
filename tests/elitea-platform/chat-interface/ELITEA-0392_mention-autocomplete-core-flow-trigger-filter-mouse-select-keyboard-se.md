---
id: ELITEA-0392
title: "user mention autocomplete core flow: trigger, filter, mouse select, keyboard select, insert, and send"
priority: critical
type: functional
module: chat-interface
status: ready
execution_type: manual
tags: [feat:chat, r-2.0.3, r-2.0.7]
requirements: [EliteaAI/elitea_issues#4896, EliteaAI/elitea_issues#4921, EliteaAI/elitea_issues#6368]
---
# ELITEA-0392: user mention autocomplete core flow: trigger, filter, mouse select, keyboard select, insert, and send

**Module:** Chat Interface · **Priority:** Critical · **Type:** Functional

**Objective:** Verify the full user mention autocomplete flow in a single sequential run — from triggering the dropdown, filtering suggestions by typing, selecting a participant via mouse, re-triggering and selecting via keyboard, inserting both mentions, and successfully sending the message.

**Coverage:**
- Typing `+` triggers the user mention autocomplete dropdown listing all user participants
- Typing after `+` filters suggestions in real time to matching names only
- Mouse click on a suggestion inserts the mention and closes the dropdown — existing input text is preserved (not replaced)
- ArrowDown/ArrowUp navigation + Enter confirmation inserts a second mention via keyboard — first mention is preserved (not replaced)
- Dropdown re-triggers after inserting a first mention and continuing to type
- Both mentions are correctly present in the submitted message and rendered in conversation history

## Preconditions

- Logged into ELITEA at {{base_url}}
- Team project opened
- A conversation is open with at least 2 participants (e.g., "Alice" and "Bob") listed in the participants panel
- Chat message input field is visible and empty

## Test Data

| Data | Value |
|---|---|
| Participant 1 | "Alice" |
| Participant 2 | "Bob" |
| Filter string | `Al` |
| Final composed message | `Hi @Alice and @Bob, please review.` |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the conversation; click the chat message input field | Input field is focused and empty |
| 2 | Type `+` | User mention autocomplete dropdown appears near the cursor listing all participants: "Alice", "Bob" |
| 3 | Type `Al` (input is now `+Al`) | Dropdown narrows to show only "Alice"; "Bob" is no longer listed |
| 4 | Click "Alice" in the dropdown | Dropdown closes; `@Alice` is inserted into the input field at cursor position |
| 5 | Type ` and ` (input is now `@Alice and `) | Text is appended normally; no dropdown appears yet |
| 6 | Type `+` | Autocomplete dropdown re-appears listing all participants: "Alice", "Bob" |
| 7 | Press Arrow Down once to highlight "Bob", then press Enter | Dropdown closes; `@Bob` is inserted; input reads `@Alice and @Bob` |
| 8 | Type `, please review.` to complete the message | Input reads `@Alice and @Bob, please review.` |
| 9 | Click Send (or press Enter) | Message is submitted successfully |
| 10 | Verify the sent message in the conversation history | `@Alice and @Bob, please review.` is visible with both mentions correctly rendered |

## Expected Final State

`@Alice and @Bob, please review.` is visible with both mentions correctly rendered

## Pass/Fail Criteria

**Pass:**
- Dropdown appears on each `@` keystroke and disappears after selection
- Filter correctly narrows suggestions after each typed character
- Mouse click and ArrowDown+Enter each insert the correct participant mention at cursor position — all pre-existing text is preserved
- Both mentions are present and correctly rendered in the sent message

**Fail:**
- Dropdown does not appear on `@`
- Filter does not narrow the list
- Either selection method fails to insert the mention or leaves the dropdown open
- Selecting a mention replaces/clears all existing input content instead of appending (bug EliteaAI/elitea_issues#4921)
- Message is missing one or both mentions, or fails to send
