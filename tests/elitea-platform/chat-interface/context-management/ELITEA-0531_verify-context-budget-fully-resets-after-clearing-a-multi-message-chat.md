---
id: ELITEA-0531
title: "Verify Context Budget Fully Resets After Clearing a Multi-Message Chat with Tools and Agent Calls"
priority: high
type: functional
module: context-management
status: ready
execution_type: manual
tags: [nfr:usability, eng:frontend, ui]
requirements: [ProjectAlita/projectalita.github.io#3927]
---
# ELITEA-0531: Verify Context Budget Fully Resets After Clearing a Multi-Message Chat with Tools and Agent Calls

**Module:** Context Management · **Priority:** High · **Type:** Functional

**Objective:** Verify that the context budget display fully clears (no stale messages, summaries, or token usage) after clearing chat context on a session containing regular messages, tool calls, and agent calls — and remains clear after a page reload and the first new message.

**Coverage:**
- Context budget state after a rich chat session (multiple regular messages + tool calls + agent calls)
- Context budget state immediately after clearing the chat context
- Context budget state after refreshing the page (persistent stale data scenario)
- Context budget state after sending the first new message post-clear (mixed old + new values scenario)

## Preconditions

- User is logged in to ELITEA (Dev or Stage environment)
- A Chat session is open with at least one Tool and one Agent attached
- The chat has been actively used:
  - At least 5 regular user/assistant message exchanges have been sent (e.g., "What is 2+2?", "Summarize this topic", "List 3 ideas", "Translate hello to Spanish", "What is today's date?")
  - At least 2 distinct tool calls have been invoked (e.g., search tool, code execution tool)
  - At least 1 agent call has been made within the session
- Context budget panel is expanded and visible, showing non-zero values (message count, token usage)
- Browser: Chrome (latest stable)

## Test Data

| Item | Value |
|---|---|
| Environment | Dev: {{base_url}} / Stage: {{base_url}} |
| First post-clear message | Hello, this is a fresh start. |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Note the current context budget values: message count, summary count (if any), and total token usage. | Non-zero values are recorded for comparison. |
| 2 | Click the Clear context button in the chat interface. | Chat conversation history is cleared. |
| 3 | Observe the context budget panel immediately after clearing. | Context budget shows zero/empty values — no old messages, summaries, or token usage. |
| 4 | Reload the page (F5 / browser refresh). | Page reloads and chat interface re-renders. |
| 5 | Observe the context budget panel after reload. | Context budget still shows zero/empty values — no stale data persists. |
| 6 | Send one new message: 'Hello, this is a fresh start.' Wait for the assistant response. | Message is sent and assistant responds. |
| 7 | Observe the context budget panel after the first new message/response. | Context budget shows only values for the new message (e.g., 1 message, tokens for that single exchange). No old data from the pre-clear session appears. |

## Expected Final State

Context budget shows only values for the new message (e.g., 1 message, tokens for that single exchange). No old data from the pre-clear session appears.

## Pass/Fail Criteria

**Pass:**
- Context budget shows zero/empty values immediately after clearing
- Context budget shows zero/empty values after page reload
- After the first new message, only current session values are shown — no pre-clear data

**Fail:**
- Old message count, summary, or token usage persists after clearing
- Stale values reappear after page reload
- Old and new values appear together after the first new message
