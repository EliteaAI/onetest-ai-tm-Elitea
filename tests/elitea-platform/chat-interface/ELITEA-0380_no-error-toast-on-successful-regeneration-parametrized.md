---
id: ELITEA-0380
title: "No Error Toast on Successful Regeneration [Parametrized]"
priority: high
type: functional
module: chat-interface
status: ready
execution_type: manual
tags: [feat:chat, r-2.0.4]
requirements: [EliteaAI/elitea_issues#4721]
---
# ELITEA-0380: No Error Toast on Successful Regeneration [Parametrized]

**Module:** Chat Interface · **Priority:** High · **Type:** Functional

**Objective:** Verify that no error toast appears when regeneration succeeds — the new response is shown correctly and no false-positive notification is triggered, across Chat, Agent page, and Pipeline page.

**Coverage:**
- Regenerate completes successfully on the Chat page — no error toast
- Regenerate completes successfully on the Agent page — no error toast
- Regenerate completes successfully on the Pipeline page — no error toast
- New response replaces the previous one correctly in all cases

## Preconditions

- Logged in to {{base_url}}
- **Variant A:** A published agent is added as a participant in a Chat conversation with at least one AI response visible
- **Variant B:** An agent conversation (Agent page) has at least one AI response visible
- **Variant C:** A pipeline conversation (Pipeline page) has at least one pipeline response visible

## Test Data

| Variant | Page | Entity |
|---|---|---|
| A | Chat page | Published agent as participant |
| B | Agent page | Any agent with an active conversation |
| C | Pipeline page | Any pipeline with an active conversation |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open a conversation for the current variant (Variant A: Chat page with published agent / Variant B: Agent page / Variant C: Pipeline page) where at least one AI response is already visible. | Conversation is open. AI response is visible. |
| 2 | Click the Regenerate button on the last AI response. | Regeneration request is sent. Server returns a successful response. |
| 3 | Observe the message area after the response loads. | New response is displayed in place of the previous one. |
| 4 | Check for any toast notifications on screen. | No error toast appears. |
| 5 | Repeat steps 1–4 for the remaining variants (B and C if starting from A). | No error toast appears on successful regeneration across all three pages. |

## Expected Final State

No error toast appears on successful regeneration across all three pages.

## Pass/Fail Criteria

**Pass:**
- New response is displayed correctly
- No error toast appears after a successful regeneration

**Fail:**
- Error toast appears despite a successful regeneration (false positive)
- New response is not displayed
