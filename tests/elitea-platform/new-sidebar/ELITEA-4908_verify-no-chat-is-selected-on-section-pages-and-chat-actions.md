---
id: ELITEA-4908
title: "Verify no chat is selected on section pages and chat actions don't redirect"
priority: high
type: functional
module: new-sidebar
status: draft
execution_type: manual
tags: [r-2.0.9, eng:design, nfr:ui]
requirements: [EliteaAI/elitea_issues#7562, EliteaAI/elitea_issues#7560, EliteaAI/elitea_issues#7564]
---
# ELITEA-4908: Verify no chat is selected on section pages and chat actions don't redirect


## Preconditions

- User is logged in to `{{base_url}}`
- The selected project has at least three chats, one of them a disposable test chat

## Test Data

| Field | Value |
|-------|-------|
| Pages | Explore → Skills; Artifacts |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open a chat, then open **Explore → Skills** | The Skills page opens, and the Chats history is still in the sidebar |
| 2 | Check the Chats history | No chat is highlighted as selected |
| 3 | Delete the disposable test chat from the history | The chat is removed, and the user stays on the Skills page with no redirect |
| 4 | Click another chat in the history | That chat opens and is highlighted |
| 5 | Repeat steps 1–4 from **Artifacts** | The same behaviour |

## Expected Final State

Only an explicitly clicked chat is selected, and deleting from a non-chat page doesn't navigate.

## Pass/Fail Criteria

**Pass:**
- No chat is selected on section/Artifacts pages, delete doesn't redirect, and a click opens the chat

**Fail:**
- A chat is auto-selected, or deleting redirects the user
