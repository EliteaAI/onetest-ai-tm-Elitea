---
id: ELITEA-4556
title: "Empty tool intersection between template and toolkit silently skips injection"
priority: high
type: functional
module: web-search
status: draft
execution_type: manual
tags: [feat:admin-platform, feat:chat, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6982]
---

## Preconditions

- Ability to configure a shared Web Search toolkit whose chat-available tools exclude `web_search` and `web_extract` (e.g. only crawl/map enabled)

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Chat prompt | Any standard message |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Configure the shared Web Search toolkit so its chat-available tools do not include `web_search`/`web_extract` | Configuration saves |
| 2 | Enable the Web Search module toggle in a chat and send a message | No empty or non-functional "Web Search" toolkit appears in Participants |
| 3 | Confirm the chat proceeds normally | Chat works normally, simply without web search capability; no error shown |
| 4 | Restore a valid toolkit configuration (chat tools include `web_search`/`web_extract`) | Web Search resumes working as in test case 2 |

## Expected Final State

With an empty tool intersection, Web Search injection is silently skipped and the chat remains fully functional; restoring a valid configuration resumes normal Web Search behavior.

## Pass/Fail Criteria

**Pass:**
- No broken/empty toolkit participant appears; chat is unaffected; functionality resumes after restoring configuration

**Fail:**
- An empty or broken "Web Search" participant appears, or the chat errors out
