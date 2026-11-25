---
id: ELITEA-4546
title: "Web Search toggle ON binds search/extract tools and returns cited results across providers"
priority: critical
type: functional
module: web-search
status: draft
execution_type: manual
tags: [feat:admin-platform, feat:chat, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6982]
---

## Preconditions

- User is logged in to `{{base_url}}`
- A valid shared Tavily toolkit is resolved for the project
- At least 3 LLM providers are configured in the project (e.g. OpenAI, Anthropic, and one other)

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Chat prompt (search) | "What are today's top tech headlines?" |
| Chat prompt (extract) | A specific article URL + "Summarize this page" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | In a chat, enable the "Web Search" toggle via the Modules flyout | Switch shows ON |
| 2 | Send the search prompt | Response includes a "Web Search"/globe tool-use indicator (chip) and citations formatted as markdown links |
| 3 | Send the extract prompt with a specific URL | Model uses page extraction and the summary reflects that page's content |
| 4 | Switch the chat's LLM model to a second configured provider and repeat steps 2–3 | Web search and extraction still work; citations still appear |
| 5 | Switch to a third configured provider and repeat steps 2–3 | Web search and extraction still work for this provider too |
| 6 | Enable Web Search in an agent's Modules section and repeat the search prompt via the agent's test chat panel | Same tool-use indicator and citations appear |

## Expected Final State

Web search and page-extraction work correctly and consistently across all tested LLM providers, in both chat and agent contexts, with markdown-link citations present.

## Pass/Fail Criteria

**Pass:**
- Search and extraction succeed with every tested provider
- Citations are rendered as markdown links in all cases

**Fail:**
- Any tested provider fails to trigger web search/extraction, or citations are missing/malformed
