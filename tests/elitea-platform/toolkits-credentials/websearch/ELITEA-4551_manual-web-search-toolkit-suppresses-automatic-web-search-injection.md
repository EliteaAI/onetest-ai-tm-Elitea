---
id: ELITEA-4551
title: "Manual web-search toolkit suppresses automatic Web Search injection"
priority: critical
type: functional
module: web-search
status: draft
execution_type: manual
tags: [feat:admin-platform, feat:chat, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6982]
---

## Preconditions

- A manually configured Tavily (or equivalent web-search-flagged) toolkit is available to add as a participant

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Chat prompt | A query requiring a web search |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Add a personal/manual Tavily toolkit to a chat as a toolkit participant | Toolkit appears in Participants/Toolkits panel |
| 2 | Enable the "Web Search" module toggle in the same chat | Switch shows ON |
| 3 | Send a message requiring a web search | Only ONE web-search tool is exposed/used (the manual toolkit); no duplicate injected "Web Search" copy appears in the Participants/Toolkits panel or the tool-use indicator |
| 4 | Repeat the same setup (manual toolkit + Web Search toggle ON) on an agent and run it via its test chat panel | Same single-toolkit behavior observed; no duplication |

## Expected Final State

Only the manually added toolkit is used for web search in both chat and agent; no duplicate "Web Search" toolkit copy is injected.

## Pass/Fail Criteria

**Pass:**
- Exactly one web-search toolkit participant is visible/used in both chat and agent cases

**Fail:**
- A duplicate "Web Search" toolkit copy appears alongside the manual toolkit
