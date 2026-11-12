---
id: ELITEA-4545
title: "Web Search toggle OFF blocks all web search tool calls"
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
- Web Search is available for the current project (platform enabled, project enabled, shared toolkit resolved)

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Chat prompt | "What happened in the news today?" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open a chat in a project where Web Search is available | Chat opens normally |
| 2 | Open the Modules flyout (`+` → Modules) and ensure the "Web Search" switch is OFF | Switch shows OFF/unchecked state |
| 3 | Send the test prompt asking for current/external information | Model does not report running a web search and does not produce markdown-link citations from a live search |
| 4 | Open an agent's configuration, go to its Modules section, and ensure "Web Search" is OFF | Switch shows OFF |
| 5 | Run the agent via its test chat panel with the same prompt | Model does not perform a web search |

## Expected Final State

Neither the chat nor the agent performed any web search or returned search-derived citations while the toggle was OFF.

## Pass/Fail Criteria

**Pass:**
- No web search tool indicator/chip appears in either response
- No markdown-link citations sourced from a live search appear

**Fail:**
- A search is performed or citations appear despite the toggle being OFF
